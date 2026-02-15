        <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Live AI Trading Terminal</title>
    
    <script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    
    <style>
        :root { --bg: #0b0e11; --card: #1e2329; --accent: #f0b90b; --up: #00ff88; --down: #ff3b3b; }
        body { font-family: 'Inter', sans-serif; background: var(--bg); color: #eaecef; margin: 0; padding: 20px; }
        .header { display: flex; justify-content: space-between; align-items: center; background: var(--card); padding: 15px 25px; border-radius: 8px; margin-bottom: 20px; }
        #chart-container { width: 100%; height: 500px; border: 1px solid #363c4e; border-radius: 8px; }
        .btn-download { background: var(--accent); color: black; border: none; padding: 10px 20px; cursor: pointer; font-weight: bold; border-radius: 5px; }
        .live-indicator { display: flex; align-items: center; gap: 8px; font-size: 0.9em; color: var(--up); }
        .dot { height: 8px; width: 8px; background: var(--up); border-radius: 50%; animation: blink 1s infinite; }
        @keyframes blink { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }
    </style>
</head>
<body>

    <div id="capture-area">
        <div class="header">
            <div>
                <h2 style="margin:0">BTC/USDT <span id="price" style="color: var(--accent)">Connecting...</span></h2>
                <div class="live-indicator"><div class="dot"></div> Live WebSocket Active</div>
            </div>
            <button class="btn-download" onclick="downloadPDF()">Export PDF</button>
        </div>

        <div id="chart-container"></div>

        <div style="margin-top:20px; background: var(--card); padding: 20px; border-radius: 8px;">
            <h3>🛡️ Real-Time Strategy</h3>
            <p>Yeh chart direct <b>Binance</b> se connected hai. Green candle ka matlab hai buyers active hain.</p>
        </div>
    </div>

    <script>
        // 1. Chart Setup
        const chart = LightweightCharts.createChart(document.getElementById('chart-container'), {
            layout: { background: { color: '#0b0e11' }, textColor: '#d1d4dc' },
            grid: { vertLines: { color: '#1f222d' }, horzLines: { color: '#1f222d' } },
            timeScale: { timeVisible: true, secondsVisible: false }
        });

        const candleSeries = chart.addCandlestickSeries({
            upColor: '#00ff88', downColor: '#ff3b3b', borderVisible: false,
            wickUpColor: '#00ff88', wickDownColor: '#ff3b3b'
        });

        // 2. WebSocket Connection (Binance)
        const symbol = 'btcusdt';
        const binanceSocket = new WebSocket(`wss://stream.binance.com:9443/ws/${symbol}@kline_1m`);

        binanceSocket.onmessage = (event) => {
            const msg = JSON.parse(event.data);
            const candle = msg.k;

            // Update Price in Header
            const priceElement = document.getElementById('price');
            priceElement.innerText = `$${parseFloat(candle.c).toLocaleString()}`;
            priceElement.style.color = candle.x ? '#f0b90b' : (parseFloat(candle.c) >= parseFloat(candle.o) ? '#00ff88' : '#ff3b3b');

            // Update Chart
            candleSeries.update({
                time: candle.t / 1000,
                open: parseFloat(candle.o),
                high: parseFloat(candle.h),
                low: parseFloat(candle.l),
                close: parseFloat(candle.c)
            });
        };

        // 3. PDF Download Function
        async function downloadPDF() {
            const { jsPDF } = window.jspdf;
            const element = document.getElementById('capture-area');
            const canvas = await html2canvas(element, { backgroundColor: '#0b0e11', scale: 2 });
            const imgData = canvas.toDataURL('image/png');
            const pdf = new jsPDF('p', 'mm', 'a4');
            pdf.addImage(imgData, 'PNG', 0, 0, 210, (canvas.height * 210) / canvas.width);
            pdf.save("Live-Trade-Report.pdf");
        }

        // Resize Chart
        window.onresize = () => chart.applyOptions({ width: document.getElementById('chart-container').clientWidth });
    </script>
</body>
</html>
