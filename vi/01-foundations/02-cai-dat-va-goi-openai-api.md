# 02. Cài đặt công cụ và gọi OpenAI API

Bài này dành cho người vừa học xong bài 01, dùng được terminal, nhưng chưa từng viết code để nói chuyện với một dịch vụ AI.

Bản tiếng Việt này có để giúp người ngại đọc tiếng Anh tiếp cận được. Học xong bài này: đã cài Git, Cursor, uv, có một API key của OpenAI chạy được, và một notebook in ra câu trả lời thật từ một model trên mây.

## Mục lục

1. [Model local và API: khác nhau ở đâu](#1-model-local-và-api-khác-nhau-ở-đâu)
2. [Các công cụ cài trong bài này](#2-các-công-cụ-cài-trong-bài-này)
3. [Cài Git và GitHub Desktop](#3-cài-git-và-github-desktop)
4. [Cài Cursor](#4-cài-cursor)
5. [Cài uv](#5-cài-uv)
6. [Lấy OpenAI API key](#6-lấy-openai-api-key)
7. [Tạo project và dựng môi trường](#7-tạo-project-và-dựng-môi-trường)
8. [Đặt API key vào file .env](#8-đặt-api-key-vào-file-env)
9. [Cài extension cho Cursor](#9-cài-extension-cho-cursor)
10. [File .ipynb là gì?](#10-file-ipynb-là-gì)
11. [Chọn kernel](#11-chọn-kernel)
12. [Gọi OpenAI API lần đầu](#12-gọi-openai-api-lần-đầu)
13. [Ví dụ: hỏi về World Cup 2026](#13-ví-dụ-hỏi-về-world-cup-2026)
14. [Lỗi thường gặp](#14-lỗi-thường-gặp)
15. [Tìm trợ giúp ở đâu](#15-tìm-trợ-giúp-ở-đâu)
16. [Bảng tra nhanh](#16-bảng-tra-nhanh)

## 1. Model local và API: khác nhau ở đâu

Bài 01 chạy model ngay trên máy bằng Ollama. Model nằm trong ổ cứng, không cần mạng vẫn trả lời.

Bài này làm ngược lại. Nó gọi một model chạy trên server của OpenAI. Code gửi câu hỏi qua internet, rồi nhận câu trả lời về.

So sánh đời thường: bài 01 giống tự nấu ăn ở nhà, nguyên liệu và bếp đều của mình. Bài này giống gọi món ở nhà hàng lớn, đầu bếp giỏi nấu giúp, nhưng phải trả tiền và phải đặt qua mạng.

| | Model local (bài 01) | API (bài này) |
| --- | --- | --- |
| Model chạy ở đâu | Trên máy | Trên server OpenAI |
| Cần mạng không | Không | Có |
| Chi phí | Miễn phí | Trả tiền theo lượt dùng |
| Chất lượng model | Bị giới hạn bởi máy | Model lớn, mạnh |
| Riêng tư | Dữ liệu ở trong máy | Dữ liệu gửi cho OpenAI |

Cả hai cách đều có chỗ dùng. Local thì riêng tư và miễn phí. API cho dùng model mạnh mà không cần máy mạnh.

> API tính tiền theo từng lần gọi. Khi học thì số tiền rất nhỏ, thường chỉ vài phần của một xu mỗi lần. Nhưng vẫn phải nạp tiền trước. Xem mục 6.

## 2. Các công cụ cài trong bài này

Cài một lần. Đây là bộ đồ nghề chuẩn cho mọi project Python về AI sau này.

| Công cụ | Là gì | Vì sao cần |
| --- | --- | --- |
| **Git** | Phần mềm quản lý phiên bản | Lưu lại lịch sử thay đổi của code |
| **GitHub** | Trang web lưu trữ project Git | Cất và chia sẻ code trên mạng |
| **GitHub Desktop** | App bấm nút thay cho gõ lệnh Git | Dùng Git mà không cần gõ lệnh |
| **Cursor** | Trình soạn code có AI sẵn bên trong | Viết và chạy code |
| **uv** | Trình quản lý thư viện Python | Cài Python và thư viện rất nhanh |

> Cursor là trình soạn code dựng trên VS Code, gắn thêm một trợ lý AI. Cái gì chạy được trên VS Code thì cũng chạy được trên Cursor.

## 3. Cài Git và GitHub Desktop

### Git là gì?

**Git** là phần mềm ghi lại lịch sử của một project. Nó lưu các bản chụp của code để sau này lấy lại bản nào cũng được. Git chạy ngay trên máy.

So sánh: Git giống tính năng lưu lịch sử chỉnh sửa trong Google Docs. Lỡ làm hỏng vẫn quay về bản cũ được.

### GitHub là gì?

**GitHub** là trang web cất các project Git trên mạng. Đây là chỗ code nằm trên mây, để sao lưu và chia sẻ. Tài khoản miễn phí là đủ.

### GitHub Desktop là gì?

**GitHub Desktop** là app làm các thao tác Git bằng cách bấm nút thay vì gõ lệnh. Đây là cách dễ nhất để cất code lên GitHub. Cài nó cũng tự cài luôn Git.

### Các bước

1. Tạo tài khoản GitHub miễn phí tại <https://github.com>
2. Tải GitHub Desktop tại <https://desktop.github.com>
3. Cài rồi đăng nhập bằng tài khoản GitHub.
4. Cài GitHub Desktop là tự cài luôn Git, nên không cần cài Git riêng.

Kiểm tra Git đã cài chưa. Mở terminal rồi chạy:

```bash
git --version
```

Hiện ra số phiên bản là Git đã sẵn sàng.

## 4. Cài Cursor

**Cursor** là trình soạn code dùng cho cả hành trình còn lại. Nhìn và dùng y như VS Code, có thêm trợ lý AI ở bên cạnh.

1. Tải Cursor tại <https://cursor.com>
2. Cài rồi mở thử một lần.
3. Đăng nhập khi được hỏi. Gói miễn phí là đủ để bắt đầu.

> Ai đang dùng VS Code thì xài luôn cũng được. Các extension và các bước y hệt. Chọn Cursor làm mặc định vì nó có sẵn trợ giúp AI bên trong.

## 5. Cài uv

**uv** là công cụ vừa cài Python vừa quản lý thư viện cho project. Nó nhanh và lo giúp những phần rối rắm. Mỗi project được uv tạo một không gian riêng để các thư viện không đụng nhau.

So sánh: uv giống người quản kho. Mỗi project là một kho riêng, đồ của kho nào ở yên kho đó, không lẫn lộn.

### Windows

Mở PowerShell rồi chạy:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### Mac

Mở app Terminal rồi chạy:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Đóng terminal, mở một cái mới, rồi kiểm tra:

```bash
uv --version
```

> uv cài luôn cả Python, nên không cần cài Python riêng. Khi project cần, uv tự tải đúng phiên bản về.

## 6. Lấy OpenAI API key

**API key** là một mật khẩu bí mật chứng minh ai đang gọi API. Code gửi kèm key này trong mỗi lần gọi để OpenAI biết tính tiền vào tài khoản nào.

So sánh: API key giống thẻ thành viên có gắn ví. Quẹt thẻ thì được phục vụ, và tiền trừ vào ví của chính chủ thẻ.

1. Tạo tài khoản tại <https://platform.openai.com>
2. Nạp một ít tiền ở mục **Billing**. Vài đô là đủ học rất nhiều.
3. Vào <https://platform.openai.com/api-keys>
4. Bấm **Create new secret key**, đặt tên, rồi copy key.
5. Lưu key vào chỗ an toàn ngay. Trang web chỉ hiện key đúng một lần.

> Coi key như mật khẩu. Đừng dán vào chỗ công khai. Đừng đẩy lên GitHub. Mục 8 chỉ cách cất key an toàn.

## 7. Tạo project và dựng môi trường

**Project** là một thư mục chứa code, các thư viện, và phần cài đặt của nó. uv tạo và quản lý thư mục này.

Mở terminal rồi chạy từng lệnh:

```bash
uv init world-cup-api
cd world-cup-api
uv add openai python-dotenv ipykernel
```

Từng lệnh làm gì:

* `uv init world-cup-api` tạo một thư mục project mới tên `world-cup-api`.
* `cd world-cup-api` đi vào thư mục đó.
* `uv add ...` cài ba thư viện vào project:
  * **openai**: thư viện chính thức để gọi OpenAI API.
  * **python-dotenv**: đọc thông tin bí mật từ file `.env`.
  * **ipykernel**: cho phép chạy notebook bên trong project này.

uv tạo một thư mục ẩn tên `.venv` trong project. Đây là **virtual environment**, một không gian riêng chứa thư viện của project. Nó giữ project này tách khỏi mọi project khác.

Giờ mở thư mục project trong Cursor:

1. Trong Cursor, chọn **File**, rồi **Open Folder**.
2. Chọn thư mục `world-cup-api`.

## 8. Đặt API key vào file .env

**File `.env`** là một file text thường, dùng để cất thông tin bí mật như API key. Code đọc từ nó, nhưng bản thân file không bao giờ lên mạng.

1. Trong Cursor, tạo một file mới trong thư mục project, tên đúng là `.env`
2. Thêm đúng một dòng, dán key thật vào sau dấu bằng:

```text
OPENAI_API_KEY=sk-dan-key-that-cua-ban-vao-day
```

3. Lưu file.

Giữ key không lên GitHub. File `.env` tuyệt đối không được đẩy lên mạng.

* `uv init` đã tạo sẵn file `.gitignore`, là file liệt kê những thứ Git cần bỏ qua.
* Mở `.gitignore` và kiểm tra có dòng `.env` chưa. Nếu thiếu, thêm vào một dòng riêng:

```text
.env
```

> Lý do: ai lấy được key là tiêu được tiền trong tài khoản. Dòng trong `.gitignore` báo Git bỏ qua file `.env`, nên key chỉ nằm yên trong máy.

## 9. Cài extension cho Cursor

**Extension** là phần cài thêm để Cursor có thêm tính năng. Cần hai cái để chạy notebook và Python.

1. Trong Cursor, bấm biểu tượng **Extensions** ở thanh bên trái. Nó trông như bốn ô vuông.
2. Tìm và cài từng cái dưới đây, cả hai đều do Microsoft phát hành:
   * **Python** (Microsoft): chạy và hiểu code Python.
   * **Jupyter** (Microsoft): chạy file notebook.
3. Bấm reload nếu Cursor hỏi.

## 10. File .ipynb là gì?

**File `.ipynb`** là một Jupyter notebook. Đây là một tài liệu trộn lẫn code chạy được với chữ và kết quả, tất cả trong một chỗ.

So sánh: notebook giống một quyển vở thí nghiệm. Ghi chú ở một dòng, làm thử ngay dòng dưới, và kết quả nằm luôn bên cạnh.

### Cách nó hoạt động

Một notebook là một chồng các **cell**. Mỗi cell thuộc một trong hai loại:

* **Code cell**: chứa code. Chạy nó là kết quả hiện ngay bên dưới.
* **Markdown cell**: chứa ghi chú, viết bằng Markdown, đúng định dạng của file `.md`.

Chạy từng cell một. Kết quả, dù là chữ, con số, hay báo lỗi, nằm gắn ngay dưới cell. Nhờ vậy notebook rất hợp để học. Sửa một cell, chạy lại, thấy ngay kết quả thay đổi.

### Có chạy trên GitHub không?

Có. GitHub hiển thị file `.ipynb` thành một trang dễ đọc. Nó cho thấy code, ghi chú, và kết quả đã lưu cùng một lúc. Nên một notebook đẩy lên GitHub trông như một bản báo cáo hoàn chỉnh, không phải code thô.

### Notebook so với Markdown

| | `.md` (Markdown) | `.ipynb` (Notebook) |
| --- | --- | --- |
| Chứa chữ | Có | Có |
| Chứa code chạy được | Không, chỉ hiện code chứ không chạy | Có, code chạy ngay tại chỗ |
| Hiện kết quả | Không | Có, lưu dưới mỗi cell |
| Hợp để làm gì | Viết và tài liệu | Thử nghiệm và học |
| Bên trong là gì | Text thường | Một file JSON |

> File `.md` là để viết cho người đọc. File `.ipynb` là để chạy code và ghi chú quanh nó. Bài này dùng notebook để mỗi lần gọi API đều chạy và hiện ra câu trả lời ngay.

## 11. Chọn kernel

**Kernel** là cái máy chạy code bên trong notebook. Notebook phải dùng kernel của project thì mới tìm thấy các thư viện đã cài.

1. Trong Cursor, tạo file mới tên `main.ipynb` trong thư mục project.
2. Mở nó. Một nút ghi **Select Kernel** hiện ở góc trên bên phải.
3. Bấm nút đó, rồi chọn **Python Environments**.
4. Chọn cái trỏ tới `.venv`, thường ghi là **.venv (Python)**.

> Kernel `.venv` chính là môi trường riêng của project ở mục 7. Chỉ nó mới có `openai` đã cài. Chọn kernel khác là gặp lỗi "module not found".

## 12. Gọi OpenAI API lần đầu

Notebook đã sẵn sàng. Giờ gửi một câu hỏi cho model.

Ở cell code đầu tiên, dán đoạn này rồi chạy:

```python
from dotenv import load_dotenv
from openai import OpenAI

# Doc key tu file .env vao moi truong
load_dotenv()

# Tao client. No tu tim OPENAI_API_KEY.
client = OpenAI()

# Gui mot cau hoi cho model
response = client.responses.create(
    model="gpt-4o-mini",
    input="Chao bang mot cau ngan."
)

# In cau tra loi cua model
print(response.output_text)
```

Từng phần làm gì:

* `load_dotenv()` nạp thông tin bí mật từ file `.env`.
* `OpenAI()` tạo ra **client**, là thứ đứng ra nói chuyện với API. Nó tự đọc key.
* `client.responses.create(...)` gửi yêu cầu đi. `model` chọn dùng AI nào. `input` là câu hỏi.
* `response.output_text` là phần chữ trả lời. `print` in nó ra.

Chạy cell. Chờ một chút, một lời chào từ model hiện ra ngay dưới cell.

> `gpt-4o-mini` là model nhỏ, rẻ, nhanh. Hợp để học. Muốn dùng model mạnh hơn sau này thì đổi giá trị `model`. Xem danh sách mới nhất tại <https://platform.openai.com/docs/models>.

## 13. Ví dụ: hỏi về World Cup 2026

Một câu hỏi thật cho thấy API làm được việc có ích. World Cup 2026 là ví dụ hay vì đây là sự kiện gần đây và có thể thức mới.

Thêm một cell mới, dán đoạn này, rồi chạy:

```python
response = client.responses.create(
    model="gpt-4o-mini",
    input=(
        "World Cup 2026 do My, Canada va Mexico dong cai. "
        "Tra loi bang ba gach dau dong ngan: "
        "nam 2026 co bao nhieu doi du, "
        "nam 2022 co bao nhieu doi du, "
        "va the thuc 2026 co gi moi."
    )
)

print(response.output_text)
```

Model trả về sự thật: 2026 có 48 đội, tăng từ 32 đội năm 2022, là kỳ World Cup lớn nhất từ trước tới nay.

Thử đổi câu hỏi. Hỏi về đội tuyển yêu thích, các thành phố đăng cai, hay lịch thi đấu. Mỗi lần chạy là gửi một yêu cầu mới và in ra câu trả lời mới.

> Model biết các sự thật chung từ lúc nó được huấn luyện, nhưng không biết kết quả đang diễn ra. Muốn biết tỉ số ngay lúc này thì chỉ mình model là chưa đủ. Các bài sau sẽ gắn thêm dữ liệu sống để khắc phục.

## 14. Lỗi thường gặp

* Quên nạp tiền vào Billing. API báo lỗi hết hạn mức (quota). Nạp vài đô ở mục Billing tại <https://platform.openai.com>.
* Chọn nhầm kernel. Lỗi "module not found" cho `openai` nghĩa là notebook chưa dùng kernel `.venv`. Chọn lại ở góc trên bên phải.
* Đặt sai tên file bí mật. Phải đúng là `.env`, có dấu chấm ở đầu và không có gì phía trước. File tên `env.txt` sẽ không nạp được.
* Đẩy nhầm file `.env` lên mạng. Kiểm tra `.gitignore` có dòng `.env` trước khi đẩy lên GitHub. Lộ key là mất tiền thật.
* Chạy cell sai thứ tự. Cell đầu tạo ra `client`. Chạy nó trước mọi cell có dùng `client`, không thì notebook báo `client` chưa được định nghĩa.
* Dán key kèm dấu cách hay dấu nháy. Dòng đúng là `OPENAI_API_KEY=sk-...`, không có dấu cách, không có dấu nháy quanh key.

## 15. Tìm trợ giúp ở đâu

* Tài liệu OpenAI API: <https://platform.openai.com/docs>
* Danh sách model và giá: <https://platform.openai.com/docs/models>
* Tài liệu uv: <https://docs.astral.sh/uv>
* Tài liệu Cursor: <https://docs.cursor.com>
* Tài liệu GitHub Desktop: <https://docs.github.com/en/desktop>

## 16. Bảng tra nhanh

### Các lệnh cài đặt

| Lệnh | Tác dụng |
| --- | --- |
| `git --version` | Kiểm tra Git đã cài chưa |
| `uv --version` | Kiểm tra uv đã cài chưa |
| `uv init <ten>` | Tạo một thư mục project mới |
| `uv add <thu-vien>` | Cài một thư viện vào project |
| `uv add openai python-dotenv ipykernel` | Cài các thư viện bài này cần |

### Toàn bộ notebook

```python
from dotenv import load_dotenv
from openai import OpenAI

load_dotenv()
client = OpenAI()

response = client.responses.create(
    model="gpt-4o-mini",
    input="Chao bang mot cau ngan."
)

print(response.output_text)
```

### Tóm tắt

> Cài Git, Cursor, uv một lần. Tạo project bằng uv, cất key vào file `.env`, và giữ file đó không lên GitHub. Mở notebook `.ipynb`, chọn kernel `.venv`, rồi chạy một cell. Code gửi câu hỏi cho OpenAI và in ra câu trả lời. Khác với model local ở bài 01, cách này chạy trên mây, tốn một ít tiền, và cho dùng model mạnh hơn nhiều.
