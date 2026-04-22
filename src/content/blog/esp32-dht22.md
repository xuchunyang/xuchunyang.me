---
title: "ESP32 + DHT22 温湿度采集"
description: "用一块 ESP32 和 DHT22 做一个最小可用的温湿度传感器，把数据推到本地 MQTT"
pubDate: 2026-04-10
tags: ["esp", "iot"]
---

这是一篇占位文章，之后会补上完整的接线图、代码和踩坑记录。

## 硬件

- ESP32-WROOM-32
- DHT22（AM2302）
- 一块面包板、几根杜邦线

## 软件

PlatformIO + Arduino framework，通过 Wi-Fi 连 MQTT broker（跑在家里 Raspberry Pi 上）。

```cpp
#include <DHT.h>
DHT dht(4, DHT22);

void setup() { dht.begin(); }
void loop()  { float t = dht.readTemperature(); /* ... */ }
```
