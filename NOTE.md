## daohuyenmy : lần đầu, tải dữ liệu từng video xem, tải từ server, lưu dữ liệu vào cache. Lần sau truy cập sẽ sử dụng cache mà k tải từ server nữa. Không tăng MB resources quá nhiều

## tiktok-test : lần đầu sẽ tải 1 loạt all dữ liệu và thêm vào cache. Lần sau sử dụng cache để xem video ( có thể tải mảnh phân rã status 206 nên tiêu tốn 1 chút MB transferred ), và có tăng MB resources nhiều khi dùng lâu

## Trong folder này chứa folder tiktok-test : là phiên bản logic khác. Lần đầu truy cập sẽ tải 1 loạt all dữ liệu video, từ lần sau sẽ dùng cache mà k tải từ server nữa. Tuy nhiên khi lướt xem sẽ ngày càng tăng bộ nhớ MB resources

## Final Code on 12/06/2025: Thêm các BASE URL để dễ dàng thay đổi domain ( chuyển tài khoản ) và thư mục gốc khi cần ( main -> gh-page )

## Final Code on 16/06/2025: Thêm BASE của CACHE_NAME, update ở phần function clearCacheAndReload().  ( const CACHE_NAME = "tiktok-clone-v1"; ). Sửa BASE URL tương đối, xử lý âm thanh, xử lý lần đầu truy cập. ID commit github: 15a659c3046d713546263cbd73ec40512225ff1d

## Final Code on 17/06/2025: Thêm logic xử lý khi video gặp lỗi, hiển thị tên video lỗi để check json fix cho dễ dàng. Thêm các thông tin cho video hiển thị trên giao diện như Title, dayCreate ( Created at )