# 01. Chạy AI trên máy local

1. [LLM là gì?](#1-llm-là-gì)
2. [Hai phần: inference engine và model](#2-hai-phần-inference-engine-và-model)
3. [Inference engine chạy local](#3-inference-engine-chạy-local)
4. [Model mã nguồn mở](#4-model-mã-nguồn-mở)
5. [Bắt đầu: cài Ollama và chạy model đầu tiên](#5-bắt-đầu-cài-ollama-và-chạy-model-đầu-tiên)
6. [Cài và chạy được bao nhiêu model cùng lúc?](#6-cài-và-chạy-được-bao-nhiêu-model-cùng-lúc)
7. [Chọn model theo cấu hình máy](#7-chọn-model-theo-cấu-hình-máy)
8. [Chạy hai model Gemma cùng lúc](#8-chạy-hai-model-gemma-cùng-lúc)
9. [Lỗi thường gặp](#9-lỗi-thường-gặp)
10. [Tìm trợ giúp ở đâu](#10-tìm-trợ-giúp-ở-đâu)
11. [Bảng tra nhanh](#11-bảng-tra-nhanh)

## 1. LLM là gì?

**LLM** = *Large Language Model* = model ngôn ngữ lớn.

Đây là bộ não AI biết đọc hiểu và viết ra chữ, giống thứ đứng sau ChatGPT, Gemini hay Claude. Gõ câu hỏi, nó trả lời.

Điều quan trọng cần nhớ ngay từ đầu: một AI hoàn chỉnh thật ra gồm **hai phần tách rời** ghép lại.

* Phần bộ não: chính là **model**.
* Phần chạy bộ não đó: chính là phần mềm, hay nói đúng hơn là **inference engine**.

Inference engine là phần mềm nạp model lên và biến câu hỏi thành câu trả lời. Hai phần này khác nhau. Đó là lý do cần hiểu cả hai.

## 2. Inference engine và model

Cách dễ hình dung nhất là **phần mềm nghe nhạc** như Windows Media Player trên Windows hoặc Music trên macOS.

| Thế giới âm nhạc | Thế giới AI |
| --- | --- |
| **App nghe nhạc** | **Inference engine** (Ollama, LM Studio...) |
| **File bài hát** (`.mp3`) | **Model AI** (Gemma, Llama...) |

Nguyên tắc cốt lõi:

> **Inference engine** giống app nghe nhạc. **Model** giống file bài hát để mở.

* Một app nghe nhạc phát được nhiều bài hát.
* Một inference engine như Ollama chạy được nhiều model khác nhau. Hôm nay Gemma, mai Qwen, tùy ý.

Cần **cả hai** mới dùng được. Có app nghe nhạc mà không có bài hát thì không nghe được gì. Có file nhạc mà không có app nghe nhạc thì cũng không mở được.

## 3. Inference engine chạy local

### Local nghĩa là gì?

**Local** nghĩa là chạy AI ngay trên máy của chính người dùng, không gửi gì lên internet.

Khác với ChatGPT (mọi thứ gõ vào đều gửi lên server của công ty ở xa), chạy local giữ **mọi thứ trong máy**.

* Riêng tư: dữ liệu không rời khỏi máy.
* Miễn phí: không trả phí hằng tháng.
* Offline: rớt mạng vẫn chạy.
* Đổi lại: tốc độ và chất lượng phụ thuộc vào sức mạnh của máy.

### Inference engine làm gì?

Nó lo hết phần kỹ thuật phức tạp.

* Tải model về máy.
* Nạp model vào bộ nhớ (RAM).
* Nhận câu hỏi và đưa cho model xử lý.
* Trả kết quả về.

### Những inference engine phổ biến

Chọn một cái để bắt đầu. Tất cả đều chạy chung các model mã nguồn mở.

| Inference engine | Giao diện | Hợp với ai |
| --- | --- | --- |
| **Ollama** | Dòng lệnh | Đơn giản, ổn định, nhẹ. Dễ cài là chạy nhất. |
| **LM Studio** | Đồ họa (GUI) | Người thích bấm chuột hơn gõ lệnh. Dễ tìm và thử model. |
| **Jan** | Đồ họa (GUI) | Bản mã nguồn mở, gọn, thay thế cho LM Studio. |
| **GPT4All** | Đồ họa (GUI) | Chạy được trên máy yếu. Có thêm tùy chọn Python. |

> Cách làm phổ biến: dùng công cụ có giao diện như LM Studio để tìm và thử model, rồi chuyển sang Ollama khi đã quen. Các công cụ nâng cao như llama.cpp, vLLM, LocalAI dành cho người chuyên sâu.

## 4. Model mã nguồn mở

### Nhắc lại: model là gì?

Model là **bộ não AI**, phần thật sự suy nghĩ và trả lời. Trong phép so sánh, nó là file bài hát mà app nghe nhạc mở.

### Mã nguồn mở (open source) nghĩa là gì?

**Mã nguồn mở** (còn gọi *open weight*) nghĩa là công ty tạo ra model công khai cho mọi người tải về dùng miễn phí, thường cho cả mục đích cá nhân lẫn thương mại.

Ngược lại là model **đóng (closed)** như GPT của OpenAI hay Claude của Anthropic. Chỉ dùng được qua dịch vụ của họ. Không tải về máy được.

> Muốn chạy AI local, bắt buộc phải dùng model mã nguồn mở. Model đóng không cho tải về.

### Vài model mã nguồn mở nổi tiếng

| Model | Made by | Ghi chú |
| --- | --- | --- |
| **Gemma** | Google | Nhẹ, hiệu quả, hợp máy yếu |
| **Llama** | Meta (Facebook) | Phổ biến, nhiều phiên bản |
| **Qwen** | Alibaba | Mạnh, hỗ trợ đa ngôn ngữ tốt (cả tiếng Việt) |
| **Phi** | Microsoft | Rất nhẹ, chạy được máy cấu hình thấp |
| **DeepSeek** | DeepSeek | Mạnh về suy luận và lập trình |
| **Mistral** | Mistral AI | Cân bằng tốt, hay dùng trong sản phẩm thực tế |

### Một model có nhiều cỡ khác nhau

Trong thư viện sẽ thấy tên kiểu `gemma3:1b`, `gemma3:4b`, `qwen3:8b`. Chữ **B** là viết tắt của *billion* (tỉ), tức **số tham số (parameters)**, hiểu nôm na là **bộ não lớn cỡ nào**.

* Số càng lớn thì càng thông minh hơn, nhưng cần máy mạnh hơn và chạy chậm hơn.
* Số càng nhỏ thì kém hơn một chút, nhưng nhẹ và nhanh trên máy yếu.

Ví dụ: `4b` nghĩa là model có 4 tỉ tham số.

> Còn một thứ tên là **quantization** (thường thấy ký hiệu `Q4`). Đây là kỹ thuật nén model cho nhẹ đi để chạy được trên máy thường. Inference engine như Ollama tự làm việc này, nên không cần lo.

## 5. Bắt đầu: cài Ollama và chạy model đầu tiên

Làm theo các bước dưới đây. Làm xong là đã cài Ollama và đang chat với một model thật.

### Bước 1: Cài Ollama

#### Windows

1. Vào <https://ollama.com/download>
2. Tải file cài cho Windows (`OllamaSetup.exe`) rồi chạy nó.
3. Cài xong, Ollama chạy ngầm trong máy. Mở **PowerShell** (hoặc Command Prompt) để gõ lệnh.

Nếu chưa biết mở PowerShell hoặc Command Prompt:

1. Nhấn phím **Windows** trên bàn phím, hoặc bấm nút **Start** ở góc dưới màn hình.
2. Gõ `PowerShell` rồi nhấn **Enter** để mở PowerShell.
3. Nếu muốn dùng Command Prompt, gõ `cmd` rồi nhấn **Enter**.
4. Khi cửa sổ hiện ra, gõ các lệnh như `ollama --version`.

![Mở PowerShell hoặc Command Prompt trên Windows](../../images/0101.png)

#### Mac

1. Vào <https://ollama.com/download>
2. Tải bản cho macOS, mở file `.zip`, kéo **Ollama** vào thư mục Applications.
3. Mở nó một lần (nó hiện ở thanh menu trên cùng). Sau đó mở app **Terminal** để gõ lệnh.

Kiểm tra đã cài đúng chưa (lệnh giống nhau trên cả hai):

```bash
ollama --version
```

### Bước 2: Xem các model mã nguồn mở có sẵn

Ollama có một thư viện model công khai để tải về.

* Xem trên web: vào <https://ollama.com/library> để thấy tất cả model, các cỡ, và tên tag chính xác (như `gemma3:270m`).
* Xem model đã cài trong máy:

```bash
ollama list
```

Lưu ý: `ollama list` chỉ hiện model đã có trong máy. Muốn tìm model mới để tải, dùng thư viện trên web ở trên.

### Bước 3: Cài gemma3:270m

Lệnh này tải model Gemma tí hon 270 triệu tham số của Google (khoảng 290 MB):

```bash
ollama pull gemma3:270m
```

### Bước 4: Chat với nó

```bash
ollama run gemma3:270m
```

Lệnh này mở khung chat. Gõ một câu, nhấn Enter, model trả lời. Muốn thoát chat, gõ:

```text
/bye
```

### Ví dụ trên PowerShell (Windows)

Toàn bộ quy trình trên Windows PowerShell, từ đầu đến cuối:

```powershell
# Kiem tra Ollama da cai chua
ollama --version

# Tai model Gemma ti hon
ollama pull gemma3:270m

# Xem nhung gi da cai trong may
ollama list

# Bat dau chat (go /bye de thoat)
ollama run gemma3:270m
```

Hỏi một câu mà không cần vào chế độ chat:

```powershell
ollama run gemma3:270m "Giai thich LLM la gi trong mot cau."
```

> `gemma3:270m` rất nhỏ, nên hỏi ngắn và đơn giản. Muốn câu trả lời tốt hơn, cài một model lớn hơn sau (xem mục 7) và chạy y hệt cách trên.

## 6. Cài và chạy được bao nhiêu model cùng lúc?

Đây là ba câu hỏi khác nhau mà người mới hay lẫn lộn.

### a) Cài (tải về): gần như không giới hạn

Cài một model chỉ là **lưu file của nó vào ổ cứng**. Giới hạn duy nhất là **dung lượng ổ cứng**.

Mỗi model nhỏ chỉ vài GB. Một ổ bình thường chứa được hàng chục, thậm chí hàng trăm model. Chúng chỉ nằm yên trên ổ và **không tốn RAM** khi chưa chạy. Theo phép so sánh nghe nhạc: đây là số bài hát lưu trong máy.

### b) Chạy cùng lúc: giới hạn bởi bộ nhớ

Để thật sự chạy, model phải được **nạp vào bộ nhớ** (RAM nếu dùng CPU, hoặc VRAM nếu dùng GPU). Bộ nhớ thì có hạn.

Ollama có thể nạp nhiều model cùng lúc. Mặc định nó cho phép tối đa 3 model nạp đồng thời trên máy chạy CPU. Nhưng điều này chỉ được nếu chúng vừa đủ trong bộ nhớ khả dụng. Chính điều kiện đó là giới hạn thật.

Con số 3 chỉ là trần cho phép. **Giới hạn thật là bộ nhớ.** Máy mạnh chạy được vài cái cùng lúc. Máy yếu chỉ chạy một.

### c) Chuyển qua lại giữa các model: inference engine tự lo

Không phải tự đóng hay mở model. Ollama tự quản lý. Nếu một yêu cầu cần model mới mà bộ nhớ không đủ, Ollama **tự bỏ nạp các model đang rảnh để dọn chỗ**, rồi nạp model mới.

Khi gọi model A, nó nạp A. Khi gọi model B mà bộ nhớ không chứa nổi cả hai, nó âm thầm bỏ A và nạp B. Quá trình này diễn ra ngầm và chỉ tốn vài giây nạp lại. Dùng lệnh `ollama ps` để xem model nào đang trong bộ nhớ.

## 7. Chọn model theo cấu hình máy

Yếu tố quan trọng nhất là **bộ nhớ**: RAM hệ thống nếu không có card đồ họa rời, hoặc **VRAM** (bộ nhớ trên GPU rời) nếu có. GPU nhanh hơn CPU rất nhiều cho việc này. Model nào vừa trong VRAM sẽ chạy mượt hơn hẳn. Luôn dùng bản quantization mặc định **Q4** để tiết kiệm bộ nhớ.

Dưới đây là bốn nhóm máy phổ biến. Tìm nhóm gần nhất với máy đang dùng.

### Nhóm 1: Không có GPU rời (chỉ CPU và RAM)

Laptop văn phòng, máy bàn đời cũ, máy chỉ có card tích hợp. Mọi thứ chạy bằng CPU, được nhưng chậm. Giữ model nhỏ.

* Vùng ngon nhất: model **1B đến 4B**, ví dụ `gemma3:1b`, `gemma3:4b`, `llama3.2:3b`, `qwen3:4b`
* Chạy được nhưng chậm: một model **7B đến 8B**, ví dụ `qwen3:8b`
* Tránh: mọi thứ lớn hơn

### Nhóm 2: GPU phổ thông và tầm trung (khoảng 6 đến 8 GB VRAM)

Nhiều laptop gaming và card bàn giá tốt, ví dụ dòng RTX 3050 hoặc 3060.

* Thoải mái: model **7B đến 8B**, ví dụ `qwen3:8b`, `llama3.1:8b`, `phi-4`
* Có thể: lên tới khoảng **12B đến 14B** (bản nén), ví dụ `gemma3:12b`

### Nhóm 3: GPU cao cấp (khoảng 16 đến 24 GB VRAM)

Card bàn cho dân chơi, ví dụ dòng RTX 3090 hoặc 4090.

* Thoải mái: model **27B đến 32B**, ví dụ `gemma3:27b`, `qwen2.5-coder:32b`
* Được nhưng chậm hơn: model **70B** ở mức Q4, ví dụ `llama3.3:70b`

### Nhóm 4: Mac chip Apple Silicon (dòng M, bộ nhớ hợp nhất)

Trên các máy Mac này, CPU và GPU **dùng chung bộ nhớ**. Tổng RAM là thứ quyết định. Chúng mạnh đáng ngạc nhiên so với kích thước.

* 16 GB RAM: thoải mái với model **7B đến 14B**
* 32 GB trở lên: chạy được model **27B đến 70B**
* **Apple MLX** thường là lựa chọn nhanh nhất trên các chip này, dù Ollama vẫn chạy tốt

### Quy tắc chung

> Chọn **model lớn nhất mà vẫn vừa bộ nhớ và còn dư chỗ**. Nếu trả lời quá chậm hoặc máy ì, lùi xuống một cỡ. Nếu chạy nhẹ nhàng, thử lên cỡ kế tiếp.

## 8. Chạy hai model Gemma cùng lúc

Một ví dụ thực tế: cài **và chạy** đồng thời cả `gemma3:270m` (model tí hon ở mục 5) lẫn `gemma3:4b` (model 4 tỉ tham số). Cách này chạy được trên hầu hết máy vì model tí hon rất nhỏ.

### Cài cả hai

Cài chỉ là tải file về ổ. Hai cái này đều nhỏ:

* `gemma3:270m`: khoảng 290 MB
* `gemma3:4b`: khoảng 3,3 GB

Tải bằng:

```bash
ollama pull gemma3:270m
ollama pull gemma3:4b
```

Xem mọi thứ đã cài trên ổ:

```bash
ollama list
```

### Chạy và gọi ra dùng

Chạy model theo tên (gõ `/bye` để thoát chat):

```bash
ollama run gemma3:270m
```

Muốn dùng cái kia:

```bash
ollama run gemma3:4b
```

### Cả hai nạp vào bộ nhớ cùng lúc được không?

Thường là được. Bộ nhớ là giới hạn khi chạy nhiều model cùng lúc, nhưng `gemma3:270m` nhỏ tới mức **cả hai vẫn vừa thoải mái** ngay cả trên máy khiêm tốn. Tính sơ: khoảng 300 MB cho cái tí hon cộng khoảng 4 GB cho cái 4b, tổng dưới 5 GB. Ollama mặc định cho phép nạp tới 3 model cùng lúc trên máy CPU, nên nó giữ cả hai trong bộ nhớ khi cả hai đang dùng.

Xem model nào đang nằm **trong bộ nhớ** (không phải chỉ cài trên ổ):

```bash
ollama ps
```

Lệnh này hiện từng model đang nạp, kích thước, và bộ đếm ngược tới lúc tự bỏ nạp. Ollama giải phóng một model sau khoảng 5 phút không dùng.

### Vì sao cặp này hữu ích

* Dùng `gemma3:270m` cho việc nhanh, đơn giản. Cực nhanh nhưng chất lượng hạn chế.
* Dùng `gemma3:4b` khi cần câu trả lời tốt hơn. Chậm hơn nhưng thông minh hơn rõ. Đây là model chính hằng ngày.

Mở hai cửa sổ terminal, mỗi cái chạy một model, chúng cùng nằm trong bộ nhớ. Hoặc chỉ cần `run` cái nào cần và để Ollama tự lo việc nạp và bỏ nạp.

## 9. Lỗi thường gặp

* Chạy model lớn hơn bộ nhớ khả dụng. Máy ì hẳn hoặc model không nạp được. Chọn cỡ nhỏ hơn, và dùng `ollama ps` để xem đang nạp gì.
* Bỏ quên tag cỡ. `ollama run gemma3` tải về bản mặc định, có thể rất lớn. Luôn ghi tag chính xác, ví dụ `gemma3:270m`.
* Trông đợi model tí hon trả lời như ChatGPT. `gemma3:270m` nhanh nhưng hạn chế. Lên `gemma3:4b` để có câu trả lời tốt hơn.
* Quên rằng model còn nằm trong bộ nhớ. Ollama giữ model khoảng 5 phút sau lần dùng cuối. Kiểm tra bằng `ollama ps`.
* Đóng terminal và tưởng Ollama dừng theo. Ollama chạy ngầm như một dịch vụ. Model tự bỏ nạp sau một lúc không dùng.

## 10. Tìm trợ giúp ở đâu

* Trang tải và tài liệu chính thức: <https://ollama.com>
* Danh sách đầy đủ model kèm cỡ và tag: <https://ollama.com/library>
* Mã nguồn và nơi báo lỗi: <https://github.com/ollama/ollama>
* Chạy `ollama help` để xem toàn bộ danh sách lệnh.

## 11. Bảng tra nhanh

### Inference engine và model

| | Inference engine | Model mã nguồn mở |
| --- | --- | --- |
| **Là gì?** | Công cụ chạy AI | Bộ não AI |
| **Ví dụ** | Ollama, LM Studio, Jan, GPT4All | Gemma, Llama, Qwen, Phi |
| **Tương tự** | App nghe nhạc | File bài hát |
| **Cài bao nhiêu?** | Một cái là đủ | Tải về bao nhiêu tùy ý |
| **Quyết định gì?** | Cách tương tác (CLI hay GUI) | Model thông minh đến đâu |

### Các lệnh Ollama cơ bản

| Lệnh | Tác dụng |
| --- | --- |
| `ollama --version` | Kiểm tra Ollama đã cài chưa |
| `ollama pull <model>` | Tải model (ví dụ `gemma3:270m`) |
| `ollama list` | Xem các model đã cài trong máy |
| `ollama run <model>` | Bắt đầu chat với model |
| `ollama ps` | Xem model nào đang nạp trong bộ nhớ |
| `/bye` | Thoát chat |

### Cỡ model theo cấu hình máy

| Cấu hình máy | Cỡ model thoải mái |
| --- | --- |
| Không có GPU (chỉ CPU và RAM) | 1B đến 4B |
| GPU phổ thông và tầm trung (6 đến 8 GB VRAM) | 7B đến 8B |
| GPU cao cấp (16 đến 24 GB VRAM) | 27B đến 32B (lên tới 70B) |
| Mac chip Apple Silicon | 7B đến 70B tùy theo RAM |
