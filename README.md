# ITAES Dashboard — WebGIS Command Center

Giao diện điều hành dành cho **13 hệ thống WebGIS** trong danh mục ITAES, dựng bằng HTML/CSS/JavaScript thuần, không cần build hoặc backend.

## Nguyên tắc bảo toàn file gốc

- `original/ITAES-Dashboard-13-WebGIS.html` là **file HTML do người dùng cung cấp, được giữ nguyên nội dung**. Không chỉnh sửa CSS, JavaScript, cấu trúc DOM của file này.
- `index.html` là giao diện **dashboard wrapper** riêng biệt. Khi bấm một thẻ, Dashboard chuyển sang chế độ Workspace và hiển thị trang đích trong `<iframe>`; mã nguồn trang đích không bị sửa.
- Dashboard mới có danh mục 13 hệ thống, tìm kiếm, lọc theo lĩnh vực, điều hướng nhanh, tải lại, toàn màn hình, sao chép URL, mở trang gốc và deep-link `#sysname`.
- Các mục trong bản gốc được giữ đúng thứ tự và tên; nhóm chủ đề chỉ là cách phân loại bổ sung của dashboard wrapper.

## Cấu trúc

```text
index.html                                   # Dashboard mới
original/ITAES-Dashboard-13-WebGIS.html      # Dashboard HTML do người dùng cung cấp (KHÔNG THAY ĐỔI)
systems/                                    # Tùy chọn: đặt nguyên bản HTML từng WebGIS tại đây
  truotlohsp.html
  airpollution.html
  bacduong.html
  binhdinh.html
  detectstorm.html
  dienbien.html
  drought.html
  koreanvietnam.html
  quangtri.html
  songda.html
  tpdienbien.html
  vgtb.html
  livinglab.html
```

**Lưu ý:** Thư mục `systems/` là tùy chọn và **chưa có** 13 tệp HTML hệ thống trong repository. Chúng cần được cấp bởi người quản trị hoặc chủ sở hữu nguồn, nếu muốn lưu cục bộ. Không sử dụng bản demo hay placeholder thay cho trang WebGIS thật.

## Cơ chế nhúng WebGIS

1. Nếu là **Dashboard HTML gốc**, iframe dùng đường dẫn `original/ITAES-Dashboard-13-WebGIS.html`.
2. Nếu có `systems/<sysname>.html` và máy chủ trả về HTML hợp lệ, iframe ưu tiên tệp đó. Tệp được hiển thị nguyên bản, chỉ thay đổi vùng chứa.
3. Nếu không có bản local, thử `https://itaes.vn/<sysname>.html`.
4. Nút **Mở trang nguồn** dùng đường dẫn gốc được ghi trong HTML đính kèm: `http://itaes.vn/<sysname>.html`.

### Giới hạn cần biết

- GitHub Pages chạy HTTPS. Việc nhúng đường dẫn HTTP có thể bị trình duyệt chặn do mixed content. Vì vậy dashboard thử phiên bản HTTPS; **không xác nhận được các trang HTTPS hiện đang khả dụng**.
- Website nguồn có thể chặn nhúng bằng `X-Frame-Options` hoặc `Content-Security-Policy: frame-ancestors`. Không thể vượt qua hạn chế này chỉ bằng JavaScript phía trình duyệt và không nên cố vượt qua.
- Tệp HTML độc lập có thể vẫn tải API, bản đồ, cookie hoặc tài nguyên từ những máy chủ khác. Đặt một tệp HTML trong repository **không đồng nghĩa** toàn bộ ứng dụng WebGIS hoạt động offline.
- Dashboard không tuyên bố các hệ thống online nếu chưa có kiểm tra hợp lệ. `fetch(...,{mode:'no-cors'})` không đủ để xác nhận trang hoạt động đúng.

## Kích hoạt GitHub Pages

Vào **Settings → Pages** của repository, chọn **Deploy from a branch** → branch **main**, folder **/(root)** → **Save**. Sau khi GitHub xuất bản xong, trang dự kiến là:

https://base27-cvnss.github.io/-ITAES-/

Nếu Pages chưa được bật, URL này sẽ chưa hoạt động.

## Sử dụng

Mở `index.html` qua máy chủ HTTP tĩnh hoặc GitHub Pages. Chọn thẻ hệ thống để xem trong Dashboard; dùng **Tổng quan** để quay lại. Cũng có thể truy cập theo hash, ví dụ `#airpollution` hoặc `#original`.

> ITAES Dashboard wrapper · 2026. Dữ liệu nguồn và quyền sử dụng đối với mỗi ứng dụng WebGIS tuân theo điều kiện của chủ sở hữu ứng dụng.
