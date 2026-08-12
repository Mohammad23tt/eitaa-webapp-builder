# مرجع سریع متدها و اشیاء SDK ایتا

## اشیاء اصلی

- `window.Eitaa.WebApp` — نقطه ورود اصلی
- `initData` (string) — داده خام برای اعتبارسنجی سمت سرور
- `initDataUnsafe` (object) — داده پارس‌شده (غیرقابل اعتماد)
- `version`, `platform`, `colorScheme`, `themeParams`
- `isExpanded`, `isFullscreen`, `viewportHeight`, `viewportStableHeight`
- `MainButton`, `BackButton`, `SecondaryButton`, `SettingsButton`
- `HapticFeedback`, `Accelerometer`, `Gyroscope`, `DeviceOrientation`

## متدهای پرکاربرد

```js
webApp.ready()
webApp.expand()
webApp.close()
webApp.enableClosingConfirmation()
webApp.disableClosingConfirmation()
webApp.enableVerticalSwipes()
webApp.disableVerticalSwipes()

webApp.setHeaderColor('#RRGGBB' | 'bg_color' | 'secondary_bg_color')
webApp.setBackgroundColor(...)
webApp.setBottomBarColor(...)

webApp.showAlert(message)
webApp.showConfirm(message, callback)
webApp.showPopup({title, message, buttons}, callback)

webApp.requestContact(callback)  // (success, data) => {}

webApp.openLink(url, options)
webApp.openEitaaLink(link)  // اگر موجود باشد

webApp.onEvent(eventType, handler)
webApp.offEvent(eventType, handler)
```

## رویدادهای مهم

- `themeChanged`
- `viewportChanged` (با isStateStable)
- `mainButtonClicked`
- `backButtonClicked`
- `settingsButtonClicked`

## MainButton نمونه

```js
webApp.MainButton.setText('شروع بازی');
webApp.MainButton.setParams({
  color: '#2481cc',
  text_color: '#ffffff',
  is_active: true,
  is_visible: true
});
webApp.MainButton.onClick(() => { /* ... */ });
webApp.MainButton.show();
```

## نکات امنیتی

- فقط `initData` را به سرور بفرست و آنجا hash را با توکن برنامه چک کن.
- هرگز توکن برنامه را در فرانت‌اند قرار نده.
