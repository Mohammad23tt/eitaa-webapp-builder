# قالب سریع برنامک ایتا

## index.html

```html
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>برنامک من</title>
  <script src="https://developer.eitaa.com/eitaa-web-app.js"></script>
  <link href="https://cdn.jsdelivr.net/gh/rastikerdar/vazirmatn@v33.003/Vazirmatn-font-face.css" rel="stylesheet">
  <style>
    :root {
      --bg: var(--tg-theme-bg-color, #ffffff);
      --text: var(--tg-theme-text-color, #000000);
      --button: var(--tg-theme-button-color, #2481cc);
      --button-text: var(--tg-theme-button-text-color, #ffffff);
    }
    body {
      font-family: Vazirmatn, Tahoma, sans-serif;
      margin: 0;
      padding: 16px;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      box-sizing: border-box;
    }
    button {
      background: var(--button);
      color: var(--button-text);
      border: none;
      padding: 12px 24px;
      border-radius: 12px;
      font-size: 16px;
      cursor: pointer;
      width: 100%;
      margin-top: 12px;
    }
  </style>
</head>
<body>
  <h1 id="greeting">سلام!</h1>
  <p id="user-info">در حال بارگذاری...</p>
  <button id="action-btn">اقدام اصلی</button>
  <button id="close-btn">بستن</button>

  <script src="app.js"></script>
</body>
</html>
```

## app.js

```js
document.addEventListener('DOMContentLoaded', () => {
  const webApp = window.Eitaa?.WebApp;
  if (!webApp) {
    document.getElementById('user-info').textContent = 'این برنامه فقط داخل ایتا کار می‌کند.';
    return;
  }

  webApp.ready();
  webApp.expand();

  // نمایش نام کاربر (فقط برای نمایش — اعتبارسنجی واقعی سمت سرور)
  const user = webApp.initDataUnsafe?.user;
  if (user) {
    document.getElementById('greeting').textContent = `سلام ${user.first_name || ''}!`;
    document.getElementById('user-info').textContent = `شناسه: ${user.id}`;
  }

  // دکمه اصلی پایین صفحه ایتا
  webApp.MainButton.setText('ادامه');
  webApp.MainButton.onClick(() => {
    webApp.showAlert('دکمه اصلی کلیک شد!');
  });
  webApp.MainButton.show();

  document.getElementById('action-btn').addEventListener('click', () => {
    webApp.showConfirm('آیا مطمئن هستید؟', (ok) => {
      if (ok) webApp.HapticFeedback?.notificationOccurred('success');
    });
  });

  document.getElementById('close-btn').addEventListener('click', () => {
    webApp.close();
  });

  // پشتیبانی از تغییر تم
  webApp.onEvent('themeChanged', () => {
    // استایل‌ها از CSS variables به‌روز می‌شوند
  });
});
```

این قالب آماده استقرار روی هر هاست HTTPS است.
