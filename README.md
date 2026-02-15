# trading-candel-chart-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Live Crypto Tracker</title>
    <script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    
    <style>
        body { font-family: sans-serif; background: #0b0e11; color: #eaecef; margin: 0; padding: 20px; }
        #chart { width: 100%; height: 500px; margin-top: 20px; border: 1px solid #363c4e; }
        .header { display: flex; justify-content: space-between; align-items: center; background: #1e2329; padding: 10px 20px; border-radius: 5px; }
        .btn-download { background: #f0b90b; color: black; border: none; padding: 10px 15px; cursor: pointer; font-weight: bold; border-radius: 4px; }
        .status { color: #00ff88; font-size: 0.9em; }
    </style>
</head>
<body>

    <div class="header">
        <div>
            <h2 style="margin:0">BTC/USDT <span id="price" style="color:#f0b90b">Loading...</span></h2>
            <span class="status">● Live Connection Active</span>
        </div>
        <button class="btn-download" onclick="downloadPDF()">Download PDF Report</button>
    </div>

    <div id="chart"></div>

    <div style="margin-top:20px; background:#1e2329; padding:15px; border-radius:5px;">
        <h3>📊 Current Strategy: Scalping 1-Min</h3>
        <p>Agar Candle Green hai aur volume high hai, toh momentum upward hai. PDF download karke aap apni entry points mark kar sakte hain.</p>
    </div>

    <script>
        // 1. Chart Setup
        const chart = LightweightCharts.createChart(document.getElementById('chart'), {
            layout: { background: { color: '#0b0e11' }, textColor: '#d1d4dc' },
            grid: { vertLines: { color: '#1f222d' }, horzLines: { color
            <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Trading Chart Pro</title>
    <script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #131722; color: white; margin: 0; padding: 20px; }
        #chart-container { width: 100%; height: 500px; background: #131722; border: 1px solid #363c4e; border-radius: 8px; }
        .controls { margin-bottom: 20px; display: flex; gap: 10px; align-items: center; }
        button { padding: 10px 20px; background: #2962ff; color: white; border: none; border-radius: 5px; cursor: pointer; font-weight: bold; }
        button:hover { background: #1e4bd8; }
        .strategy-box { margin-top: 20px; padding: 15px; background: #1e222d; border-radius: 8px; border-left: 5px solid #00ff88; }
    </style>
</head>
<body>

    <h2>📈 Pro Trading Terminal</h2>

    <div class="controls">
        <button onclick="downloadPDF()">Download Chart as PDF</button>
        <span>Symbol: <b>BTC/USDT</b></span>
    </div>

    <div id="chart-container"></div>

    <div class="strategy-box">
        <h3>🚀 Trading Strategy: Moving Average Crossover</h3>
        <p><b>Rule:</b> Jab 50-period EMA 200-period EMA ko upar se cross kare, toh yeh ek **Buy (Golden Cross)** signal hai. Agar niche cross kare toh **Sell (Death Cross)**.</p>
        <p><i>Note: Hamesha stop-loss ka istemal karein.</i></p>
    </div>

    <script>
        // Chart Initializing
        const chart = LightweightCharts.createChart(document.getElementById('chart-container'), {
            layout: { background: { color: '#131722' }, textColor: '#d1d4dc' },
            grid: { vertLines: { color: '#334155' }, horzLines: { color: '#334155' } },
        });

        const candleSeries = chart.addCandlestickSeries();

        // Dummy Data (Real data ke liye aap Binance API use kar sakte hain)
        const data = [
            { time: '2024-01-01', open: 100, high: 120, low: 90, close: 110 },
            { time: '2024-01-02', open: 110, high: 130, low: 105, close: 125 },
            { time: '2024-01-03', open: 125, high: 140, low: 120, close: 135 },
            { time: '2024-01-04', open: 135, high: 135, low: 110, close: 115 },
            { time: '2024-01-05', open: 115, high: 125, low: 112, close: 120 },
        ];
        candleSeries.setData(data);

        // PDF Download Function
        
