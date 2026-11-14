# ESP32-S3-Touch-LCD-4 LVGL 固件（微雪 4 寸 480x480）

GitHub Actions 云端编译 lvgl_micropython，产出适配微雪 ESP32-S3-Touch-LCD-4
（ESP32-S3 N16R8 / 8MB Octal PSRAM / ST7701S RGB 屏 / GT911 触摸）的固件。

- 固件里只包含 LVGL + RGB 总线框架 + GT911 驱动
- 屏幕引脚 / ST7701 初始化序列 / 界面全部在 `panel/` 的 Python 文件里，
  调参数不用重编译，直接推到板上即可

## 编译产物

Actions 跑完后：
- Artifact：`firmware`（含 firmware.bin + 编译日志）
- Release：`fw` 标签下 `firmware.bin`（公开可下载）

## 烧录

```
python -m esptool --port COM5 --baud 921600 write-flash 0 firmware.bin
```

## 上板文件

| 本地文件 | 板上路径 | 说明 |
|---|---|---|
| panel/board_panel.py | /board_panel.py | 屏幕初始化（引脚+ST7701 序列+GT911） |
| panel/panel_main.py | /main.py | 浇花面板 UI + 与旧板互联 |
