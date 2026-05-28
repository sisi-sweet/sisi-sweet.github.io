<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>搜尋測試</title>
</head>
<body>
  <h1>搜尋測試頁面</h1>
  <input type="text" id="testInput" placeholder="輸入搜尋關鍵字">
  <button onclick="testSearch()">搜尋</button>

  <div id="testResults">
    <h2>測試結果：</h2>
    <ul id="resultsList"></ul>
  </div>

  <div id="debugInfo">
    <h3>除錯資訊：</h3>
    <pre id="debugContent"></pre>
  </div>

  <script>
    const debugContent = document.getElementById('debugContent');
    const resultsList = document.getElementById('resultsList');

    function log(message) {
      const time = new Date().toLocaleTimeString();
      debugContent.textContent += `[${time}] ${message}\n`;
    }

    async function testSearch() {
      const query = document.getElementById('testInput').value;
      log(`開始搜尋: "${query}"`);

      try {
        log('載入搜尋索引...');
        const response = await fetch('/index.json');
        log(`索引載入狀態: ${response.status} ${response.statusText}`);

        if (!response.ok) {
          throw new Error(`HTTP ${response.status}: ${response.statusText}`);
        }

        const data = await response.json();
        log(`索引載入成功，共 ${data.length} 篇文章`);

        if (!query.trim()) {
          log('無輸入關鍵字');
          return;
        }

        const results = data.filter(item => {
          const title = (item.title || '').toLowerCase();
          const content = (item.content || '').toLowerCase();
          const tags = (item.tags || []).join(' ').toLowerCase();
          const keyword = query.toLowerCase();

          return title.includes(keyword) ||
                 content.includes(keyword) ||
                 tags.includes(keyword);
        });

        log(`找到 ${results.length} 筆結果`);

        // 根據 permalink 去重
        const seenPermalinks = new Set();
        const uniqueResults = [];
        for (const result of results) {
          if (!seenPermalinks.has(result.permalink)) {
            seenPermalinks.add(result.permalink);
            uniqueResults.push(result);
          }
        }

        log(`去重後：${uniqueResults.length} 筆結果`);

        resultsList.innerHTML = uniqueResults.map(item => `
          <li>
            <strong>${item.title}</strong><br>
            <small>${item.date || ''}</small><br>
            <small>${item.permalink}</small>
          </li>
        `).join('');

      } catch (error) {
        log(`錯誤: ${error.message}`);
        console.error('搜尋錯誤:', error);
      }
    }

    // 頁面載入時自動測試
    window.addEventListener('load', () => {
      log('頁面載入完成');
      log('瀏覽器 User Agent: ' + navigator.userAgent);

      // 預載入搜尋索引
      fetch('/index.json')
        .then(res => {
          log(`預載索引成功: ${res.status}`);
          return res.json();
        })
        .then(data => {
          log(`預載索引完成，共 ${data.length} 篇文章`);
        })
        .catch(err => {
          log(`預載索引失敗: ${err.message}`);
        });
    });
  </script>
</body>
</html>
