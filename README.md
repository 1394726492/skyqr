# skyqr
光遇身高查询二维码识别


# 身高查询二维码识别接口文档

## 接口地址

```
POST/GET https://height.t1qq.com/free/qrcode
```

## 请求方式

- 支持 `POST`（推荐，支持文件上传）和 `GET`（仅支持图片 URL）。

## 请求参数

### 方式一：上传图片文件

- `type`（可选）：固定为 `file`，不传默认为文件上传。
- `qr_image`（必选）：要识别的二维码图片文件，支持 JPEG、PNG、GIF 格式，最大 2MB。

#### 请求示例（curl）

```bash
curl -X POST https://height.t1qq.com/free/qrcode \
  -F "type=file" \
  -F "qr_image=@/path/to/your/qr.jpg"
```

### 方式二：通过图片 URL

- `type`（必选）：`url`
- `url`（必选）：图片的公网可访问 URL，支持 JPEG、PNG、GIF 格式，最大 2MB。

#### 请求示例（curl）

```bash
curl -G https://height.t1qq.com/free/qrcode \
  --data-urlencode "type=url" \
  --data-urlencode "url=https://height.t1qq.com/free/f4737933ef21ad9765d2879c49d97755.png"
```

---

## 成功响应示例

```json
{
  "status": "success",
  "data": {
    "height": "1.23",
    "scale": "4.56",
    "current": 0.12,
    "max": 1.34,
    "min": 7.34
  }
}
```

---

## 错误响应示例

### 1. 未上传图片或 URL

```json
{
  "status": "error",
  "message": "请上传有效的图片文件或URL"
}
```

### 2. 图片格式不支持

```json
{
  "status": "error",
  "message": "仅支持JPEG、PNG和GIF格式的图片"
}
```

### 3. 图片下载失败（URL方式）

```json
{
  "status": "error",
  "message": "图片下载失败"
}
```

### 4. 图片压缩失败

```json
{
  "status": "error",
  "message": "图片压缩失败，请尝试更小的图片"
}
```

### 5. 识别返回错误

```json
{
  "status": "error",
  "message": "二维码识别失败",
}
```

### 6. 识别结果无法解析

```json
{
  "status": "error",
  "message": "无法查询数据"
}
```

---

## 备注

- 图片大小建议不超过 1.5MB，超过会自动压缩，最大支持 2MB。
- 返回的 `height`、`scale`、`current`、`max`、`min`

## 另外免费稳定身高查询站
https://height.t1qq.com
