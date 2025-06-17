## 🚀  **Lướt video ngắm gái xinh cùng tongtrankien1605 tại xinh35** ! 🚀


**Trang được code dựa theo cấu trúc nhỏ giống Tiktok, dùng để xem các video đã được upload lên server**

<br/>

## 👉 Xem ngay [Ở ĐÂY](https://tongtrankien1605.github.io/xinh35) ạ !

</br>


## 💻 Giải thích các BASE_URL:

    const REPOSITORY_ROOT: Đường dẫn gốc của dự án, dùng để đăng ký Service Worker.
    ( ví dụ xây dựng trên github có repository là xinh35 => thì REPOSITORY_ROOT = "/xinh35/" )
              
    const VIDEOS_JSON_URL: Đường dẫn đến file JSON chứa thông tin video như Title, URL, Desription, dayCreate
    ( ví dụ xây dựng trên github có repository là xinh35 => thì const VIDEOS_JSON_URL = `${REPOSITORY_ROOT}videos.json`;

    const CACHE_NAME: Tên Cache của Worker Service, lưu ý cần cập nhật ở cả file html & script. ( const CACHE_NAME = "tiktok-clone-v1" )
            
</br> 

## ❌ Cách xóa Local Storage, Cache Service Worker, Cache HTTP:

    Settings -> Privacy and security -> Delete browsing data -> Cached images and files : Xóa Cache HTTP
    ( Cài đặt -> Quyền riêng tư và bảo mật -> Xóa dữ liệu duyệt web -> Tệp và hình ảnh được lưu trong bộ nhớ đệm )

    F12 -> Application -> Local storage : xóa Local Storage

    F12 -> Application -> Cache storage : xóa Cache Service Worker


</br>

## 😗 Một số lưu ý

</br>

    1. Xóa cache Service Worker

    Đổi CACHE_NAME trong sw.js
    -> Mục đích: Làm mới toàn bộ cache Service Worker bằng cách thay đổi tên cache, buộc tải lại tất cả tài nguyên.

    const CACHE_NAME = "tiktok-clone-v2"; // Từ v1 thành v2

    2. Thay đổi version mỗi khi cập nhật video ( video.json )
    - Cập nhật cache khi thay đổi version
    - Link video mới thêm vào cache
    - Lướt tới video mới: Load và thêm vào Service Worker
    - Link URL bị xóa: Xóa video khỏi Service Worker

    tóm tắt: 
    - Cập nhật version: Làm mới cache localStorage, tải videos.json mới.
    - Video mới: URL lưu vào localStorage, nội dung tải khi phát và lưu vào Service Worker.
    - Video bị xóa: URL không còn trong videos.json → Xóa video tương ứng khỏi cache Service Worker.
    - Băng thông: Tốn ít cho videos.json và HEAD request; video mới chỉ tải khi xem, video cũ dùng cache nếu còn trong danh sách.

    -> ( cập nhật version sẽ cập nhật cache, với link video mới sẽ thêm vào cache và khi lướt tới sẽ load và thêm vào service worker,
    còn link url nào bị xóa thì sẽ xóa video đó khỏi service worker )

    3. Cache hết hạn sau 24 giờ

    Điều kiện: Khi Date.now() >= parseInt(localStorage.getItem(CACHE_EXPIRY_KEY)), hàm isCacheValid() trả về false.

    Quy trình:

    - Bỏ qua cache localStorage vì hết hạn.
    - Fetch videos.json mới từ server (/xinh35/videos.json?v=<timestamp>).
    - Kiểm tra các URL video bằng fetch với method HEAD.
    - Lưu danh sách video mới và version vào localStorage, đặt lại thời hạn 24h.
    - Kiểm tra và xóa video cũ khỏi cache Service Worker (nếu URL không còn trong videos.json).
    - Khi lướt đến video, tải nội dung và lưu vào cache Service Worker nếu chưa có.

    Tác động:
    - Đảm bảo tải videos.json mới nếu cache hết hạn, nhưng không bắt buộc version phải thay đổi.
    - Video cũ vẫn tồn tại trong cache Service Worker nếu vẫn có trong videos.json.
    - Băng thông: Tốn cho videos.json và HEAD request; nội dung video tải khi xem (dùng cache nếu có).
