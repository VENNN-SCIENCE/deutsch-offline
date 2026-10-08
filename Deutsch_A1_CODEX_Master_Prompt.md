# PROMPT TRIỂN KHAI DEUTSCH A1 — WEBSITE HỌC TIẾNG ĐỨC OFFLINE

> Cách dùng: mở thư mục dự án trong Codex, đính kèm tài liệu PDF/MP3/ZIP hiện có và đưa toàn bộ prompt này cho Codex. Nếu có gói Deutsch_A1_Codex_Handoff trước đó, giải nén và đính kèm cùng. Đây là yêu cầu xây dựng sản phẩm chạy được, không chỉ lập kế hoạch.

## 1. Vai trò và nhiệm vụ

Bạn là kỹ sư full-stack, người thiết kế UI/UX và biên tập hệ thống học tập. Hãy xây dựng ngay một website học tiếng Đức A1 hoàn chỉnh cho người Việt, sử dụng cá nhân trên Windows 11, có backend Python, chạy trên trình duyệt qua localhost và sử dụng hoàn toàn offline sau khi cài đặt.

Người dùng là Vẹn, học Điện tử Công nghiệp, ưu tiên học tiếng Đức A1 có cấu trúc, luyện đủ nghe–nói–đọc–viết, học từ vựng qua hình ảnh và nhớ bằng thực hành. Có thể thêm nhánh từ kỹ thuật điện/tự động hóa sau nền tảng A1, nhưng không thay thế nội dung sinh hoạt cơ bản.

Hãy triển khai code, nhập dữ liệu thực, chạy ứng dụng, kiểm thử và sửa lỗi đến khi các chức năng đã công bố hoạt động. Đừng kết thúc ở một bản phân tích, design system hay dashboard demo. Hoàn thiện chức năng sản phẩm; báo riêng độ phủ nội dung đã số hóa. Nếu tài liệu thiếu ở một phần, tiếp tục các phần độc lập và ghi đúng phần bị chặn.

## 2. Phạm vi và các ràng buộc

- Backend Python + Flask; frontend HTML5/CSS3/JavaScript; dữ liệu SQLite. Có thể dùng Jinja và JavaScript module để tránh build system phức tạp. Không đổi sang giải pháp cloud để thuận tiện.
- Thiết kế desktop tốt trên laptop, dùng được trên màn hình nhỏ. Giao diện tiếng Việt, ví dụ/nội dung học tiếng Đức; không bắt người học đọc giải thích tiếng Anh.
- Máy đích Windows 11, RAM 16 GB. Không dùng mô hình AI nặng làm yêu cầu bắt buộc.
- Ứng dụng vận hành offline: mọi CSS, JS, font, ảnh, audio, thư viện render PDF cần dùng phải ở cục bộ. Không CDN, API AI/TTS cloud, telemetry hoặc tài nguyên tải khi mở bài.
- Server chỉ bind 127.0.0.1, không mở Internet hay LAN; debug tắt trong bản bàn giao. Không publish website hoặc tài liệu lên hosting trong nhiệm vụ này.
- Cài đặt ban đầu có thể dùng mạng nếu môi trường cho phép; chuẩn bị gói cài offline cho máy đích sau khi chốt phiên bản.
- Kiểm tra công cụ/skill/MCP đã có trước khi cài, không ghi đè cấu hình hay dùng API key cũ. Chỉ dùng plugin cần thiết và thực sự callable. Nếu không có Figma, tiếp tục thiết kế bằng code. Nếu có, dùng đúng hướng dẫn của plugin để thiết kế/chuyển thiết kế. Không bắt người dùng kết nối plugin mới chỉ để hoàn thành chức năng cơ bản.
- Không mặc định bạn đang điều khiển laptop Windows của người dùng. Phân biệt kiểm thử trên môi trường hiện tại và nghiệm thu thực tế trên Windows.

## 3. Tiếp nhận tài nguyên thật

Quét tài liệu được đính kèm và tạo `content/asset_manifest.json`. Mỗi tài nguyên cần ID ổn định, tên gốc, đường dẫn tương đối, loại, dung lượng, SHA-256, số trang/thời lượng nếu xác định, nguồn, trạng thái đọc/OCR, quyền sử dụng và chất lượng kiểm tra.

Ba tài nguyên mới đã được kiểm tra sơ bộ:

|Tên đính kèm|Nhận diện và vai trò|Lưu ý|
|---|---|---|
|Học từ vựng tiếng Đức qua hình ảnh và bài tập.pdf|96 trang; bìa “Deutsch lernen mit Spielen und Rätseln”; nguồn hình/chủ đề và dạng bài trò chơi|PDF không có lớp chữ; phải OCR và duyệt lại; không coi toàn sách là A1 chỉ vì nằm trong bộ A1|
|Từ điển hình ảnh tiếng Đức.pdf|174 trang; “Bildwörterbuch Deutsch – Die 1.000 wichtigsten Wörter in Bildern erklärt”, Hueber; ưu tiên cho học từ qua hình|Có lớp chữ nhưng lỗi OCR; chứa từ và hình minh họa, không có audio Đức cục bộ được xác nhận; không yêu cầu học hết 1.000 từ để đạt A1|
|Lesen und Schreiben üben A1.pdf|98 trang; Bettina Höldrich, Hueber; nguồn đọc–viết và dạng bài|97/98 trang trùng văn bản chuẩn hóa với bản “Lesen _ Schreiben A1-1.pdf” trước đó; hash khác; xử lý như bản gần trùng, chọn một bản dùng chính sau đối chiếu|

Nguồn trước đó nếu có trong tài nguyên: Goethe_A1_Wortliste để đối chiếu từ A1; Deutsch aber Hallo A1 cho bài ngữ pháp; Wortschatz Intensivtrainer cho chủ đề; Hoeren_und_Sprechen/Nghe nói A1 - PDF và 60 MP3 cho nghe–nói; Testheft studio 21 cho luyện tập khi đủ tài nguyên. Một số tài liệu A1–A2/bản đọc thử chỉ dùng bổ trợ. Kiểm tra thực tế trước sử dụng; đừng mặc định tệp thứ ba về đề thi đã được cung cấp chỉ vì được nhắc trong hội thoại.

Phải giải nén ZIP an toàn: chặn đường dẫn thoát thư mục, không thực thi file bên trong, báo mục không hỗ trợ. Bỏ Thumbs.db khỏi nội dung học. Tính hash phát hiện trùng byte; đối chiếu văn bản/trang để phát hiện gần trùng; không xóa nguồn gốc. Import chạy lại không nhân đôi bài/từ.

**Không gán số MP3 “Lesson 01” thành bài 1 hoặc CD track 1 khi chưa xác minh.** Lập bảng đối chiếu PDF trang/bài/track với file audio và đoạn thời gian. Âm thanh chưa khớp vẫn có thể nghe trong thư viện với nhãn “chưa gắn bài”. Không bịa transcript, đáp án, phiên âm, số trang hoặc phần còn thiếu của bản đọc thử.

## 4. Cấu trúc chương trình A1

Giữ khung 16 tuần, 96 buổi × 75 phút = 120 giờ nếu có curriculum cũ; có chế độ điều chỉnh thời gian học. Đây là lịch do dự án đề xuất, không phải giáo trình Goethe chính thức hay cam kết thi đỗ.

1. Làm quen, phát âm, chào hỏi, giới thiệu, đánh vần.
2. Thông tin cá nhân, số điện thoại, quốc gia, ngôn ngữ, nghề.
3. Gia đình/bạn bè; mạo từ, số nhiều, sở hữu.
4. Đồ vật, phòng, nhà ở; phủ định và mẫu câu đơn giản.
5. Ăn uống, gọi món, giá, mua thực phẩm; Akkusativ cơ bản.
6. Giờ, ngày, lịch sinh hoạt; động từ tách.
7. Học tập/công việc; modal và lịch làm việc.
8. Ôn và đánh giá A1.1 đủ bốn kỹ năng.
9. Đi lại, phương tiện, hỏi đường, bảng giờ.
10. Mua sắm/dịch vụ, kích cỡ, biểu mẫu.
11. Sức khỏe, triệu chứng đơn giản, đặt lịch.
12. Sở thích, giải trí, lời mời, thời tiết.
13. Kể về quá khứ đơn giản; Perfekt thông dụng, war/hatte.
14. Ôn tích hợp A1.2, bù điểm yếu.
15. Làm quen định dạng thi và thi thử bằng nguồn đã duyệt.
16. Thi thử khác, phản hồi và củng cố.

Mỗi tuần có mục tiêu can-do đo được, từ/chunk cần học, ngữ pháp theo tình huống, hoạt động nghe–đọc–nói–viết, ôn và đánh giá. 96 buổi là khung, không được báo tất cả đã có nội dung chỉ vì JSON có ID.

Một buổi 75 phút tham khảo: 10 ôn đến hạn, 15 đầu vào nghe/đọc, 15 thực hành có hướng dẫn, 20 nhiệm vụ giao tiếp, 10 sửa lỗi, 5 tự đánh giá. Có phiên học nhanh 10/20/30 phút để người dùng vẫn học được; không tính phiên ngắn là hoàn thành toàn buổi dài nếu chưa đạt mục tiêu.

Không lấy thứ tự trang của nhiều sách làm thứ tự học. Phân loại theo chủ đề và tiên quyết. Cấu trúc A2 như bị động hệ thống, bảng đuôi tính từ chi tiết, mệnh đề phụ phức tạp để ở thư viện mở rộng. Nội dung chuyên ngành điện là nhánh tự chọn từ tuần 7.

## 5. Học từ vựng bằng hình ảnh — chức năng trọng tâm

### 5.1 Dữ liệu một mục từ

Mỗi từ có lemma; part_of_speech; mạo từ và số nhiều nếu là danh từ; nghĩa Việt theo ngữ cảnh; ví dụ Đức/Việt; chủ đề/cấp độ; hình và mô tả; audio nếu có; nguồn/trang; trạng thái duyệt. Với động từ lưu dạng gốc và cấu trúc dùng. Không tự tạo IPA từ chữ viết nếu chưa được xác minh. Không coi các nghĩa khác nhau của một từ là cùng một thẻ bất phân biệt.

Ví dụ định dạng tự biên soạn: `die Tür – die Türen – cửa`; câu `Die Tür ist offen.` và bản dịch. Nội dung mẫu phải được kiểm tra, không gắn nhãn trích sách nếu tự viết.

### 5.2 Trải nghiệm học

Tổ chức bộ hình theo nhà/phòng, đồ dùng, thực phẩm, quần áo, cơ thể, gia đình, nghề, trường, phương tiện, thời tiết, giờ/ngày và sinh hoạt. Mỗi bộ gồm:

- Khám phá tranh: bấm vùng tương tác để hiện từ, nghĩa và ví dụ; bố trí hotspot theo tỷ lệ ảnh, thay đổi kích thước không lệch vị trí.
- Thẻ học: hình → nhớ từ → lật thẻ → kiểm tra mạo từ/số nhiều/câu ví dụ; có lựa chọn ẩn chữ và nghĩa.
- Ảnh → chọn từ: 3–4 phương án cùng loại/ngữ nghĩa hợp lý, không distractor vô lý hoặc hai đáp án cùng đúng.
- Từ → chọn ảnh: tránh ảnh mơ hồ, cảnh có nhiều vật mà không chỉ rõ đối tượng.
- Ảnh → gõ từ/mạo từ: nhập tự do, hỗ trợ bàn phím ä/ö/ü/ß; chính sách chấm umlaut/ß công khai.
- Ghép ảnh–từ: hỗ trợ bấm chọn bằng chuột/bàn phím, không chỉ kéo thả.
- Nhận diện lỗi mạo từ/số nhiều và điền từ vào câu.
- Truy hồi không có hình: nghĩa hoặc ngữ cảnh → gõ từ; kiểm tra khả năng dùng từ ngoài tranh đã học.
- Viết câu ngắn/nhiệm vụ nói dùng từ mới: dùng rubric hoặc tự đánh giá; không giả chấm tự động mọi câu.

Không bật gợi ý trước khi người học thử nhớ. Một bài có gợi ý/hình không được dùng để chứng minh đã thành thạo nếu không kiểm tra truy hồi trì hoãn. Không dùng game tính giờ làm cách luyện duy nhất; có chế độ không áp lực.

### 5.3 Xử lý hình trong PDF

Lập `image_regions` với asset_id, pdf_page 1-based, bbox, kích thước trang, file crop, hash, từ liên kết, rights/status. Ưu tiên trích ảnh nhúng hoặc render trang rồi crop chính xác. Không làm mất tỷ lệ ảnh, không upscale vô nghĩa, tạo thumbnail nhẹ và lazy-load.

Ảnh từ sách thường có chữ Đức đi kèm: ở bài kiểm tra phải dùng crop không chứa đáp án; nếu không tách được thì dùng ảnh thay thế tự tạo/có quyền hoặc không dùng ảnh đó để chấm. Không để đáp án lọt qua filename, tooltip, label hay alt-text. Trong chế độ khám phá/học, alt-text có thể mô tả đầy đủ. Với quiz dùng mô tả không tiết lộ từ Đức và cung cấp phiên bản bài không phụ thuộc thị giác; không bỏ accessibility để chống lộ đáp án.

Ảnh/đoạn sách do người dùng cung cấp chỉ đưa vào luồng sử dụng cá nhân có theo dõi nguồn/quyền. Không suy ra rằng sở hữu PDF đồng nghĩa được phân phối ảnh. Chức năng export công khai phải loại tài nguyên rights chưa xác minh và báo lý do; cho phép thay bằng minh họa tự biên soạn/có giấy phép phù hợp. Không cần dừng toàn dự án vì có tài nguyên cần xác minh quyền.

### 5.4 Lịch ôn

Triển khai SRS thực với SQLite. Cấu hình khởi tạo 1, 3, 7, 14, 30 ngày; điều chỉnh theo Again/Hard/Good/Easy, sai thì hạ khoảng ôn. Ghi loại bài, đáp án, gợi ý, thời gian và lần sai. Quy tắc cụ thể phải được tài liệu hóa/test; không gọi là FSRS nếu chưa thực sự dùng và cấu hình FSRS.

Thường 8–12 từ/chunk mới ở buổi có nội dung mới, giảm khi ôn tồn đọng. Không bắt học đủ 1.000/2.000/3.000 từ chỉ vì tiêu đề sách. Phân biệt đã xem, nhận biết, tự nhớ và dùng trong câu; không tính mở thẻ là thuộc từ. Mỗi từ có thể có hai lịch ôn nhận biết/sản sinh để tránh ghi nhớ một chiều.

## 6. Các phân hệ sản phẩm phải hoạt động

**Trang chủ:** hôm nay học gì, từ đến hạn, tiếp tục bài đang học, thời gian học thực, điểm yếu theo kỹ năng. Empty state có lời hướng dẫn; không thống kê giả, không streak chưa học.

**Lộ trình:** mục tiêu từng tuần, tiến độ bài đã published, bài chưa biên tập ghi “đang chuẩn bị”, checkpoint và lịch bù. Khóa dựa trên điều kiện rõ, cho phép người dùng điều chỉnh lộ trình. Không khóa bởi sự thiếu nội dung của hệ thống.

**Từ vựng hình ảnh:** các luồng ở mục 5, tìm kiếm từ/chủ đề, sổ từ cá nhân, đánh dấu từ khó.

**Ngữ pháp:** giải thích ngắn tiếng Việt, ví dụ Đức, bài theo ngữ cảnh, chấm câu có đáp án đã kiểm tra và giải thích lỗi. Kiểm tra lỗi trong tài liệu nguồn trước nhập.

**Nghe:** player local có tua, tốc độ, repeat đoạn; transcript chỉ hiện khi có bản đối chiếu; bài ý chính/chi tiết và luyện nhắc lại. Lưu lượt luyện. Không dùng MP3 hội thoại làm phát âm một từ rời.

**Nói:** bài giới thiệu, hỏi/đáp, yêu cầu và role-play. Ghi âm cục bộ bằng MediaRecorder nếu trình duyệt hỗ trợ và được người dùng cho phép; nghe lại, xóa, rubric/tự đánh giá. Handle mic denied/no device. Không hứa AI chấm phát âm khi chưa có engine offline được kiểm chứng. Có bản gợi ý tình huống tĩnh chạy offline; không đóng giả chatbot AI.

**Đọc–viết:** văn bản ngắn, quảng cáo, bảng giờ, menu, biểu mẫu, tin nhắn/thư. Câu khách quan tự chấm; viết tự do lưu nháp, checklist/rubric và phản hồi người đánh giá. Có đáp án mẫu sau nộp, ghi rõ mẫu không phải đáp án duy nhất.

**Luyện tập:** bộ chọn kỹ năng/chủ đề, bài ngắn, bài sai để ôn, lịch sử. Shuffle phương án giữ đúng khóa đáp án. Điểm tính từ lần trả lời đầu tiên và báo riêng luyện lại.

**Thi thử:** chỉ kích hoạt đề đã đủ nguồn, đáp án/audio và rubric. Đề chưa đủ không có nút “thi đầy đủ” giả. Tách đề khỏi kho luyện, thời gian/cách phát theo nguồn. Chỉ báo tổng điểm chính thức khi đủ phần và quy tắc được xác minh. Điểm tự đánh giá nói/viết phải ghi nhãn, không tự cấp chứng chỉ.

**Thư viện:** PDF/MP3 thật, nhóm chủ đề, mở trang cụ thể đã xác định; tìm toàn văn chỉ ở tài liệu có chữ/OCR duyệt. Liên kết bài đến nguồn.

**Thống kê:** số từ/bài đã học, ôn đến hạn, điểm từng kỹ năng, lỗi mạo từ/số nhiều, thời gian hoạt động. Không đếm tab để nền cả đêm. Không làm bảng xếp hạng giả hoặc biểu đồ đẹp từ số ngẫu nhiên.

**Cài đặt/quản lý:** hồ sơ cục bộ; chọn mục tiêu/thời gian; nhập thêm tài liệu; quản lý draft/reviewed/published; sửa câu hỏi/đáp án; sao lưu và phục hồi dữ liệu/ghi âm; xuất tiến độ JSON/CSV. Importer phải có báo cáo lỗi và dry-run.

## 7. Thiết kế giao diện có chiều sâu

Sản phẩm phải có bản sắc, phân cấp và nhịp bố cục tốt; tránh một dashboard chỉ có các ô giống nhau, nút giả và khoảng trắng vô mục đích. Sự đầy đủ đến từ luồng học và phản hồi, không từ nhồi nhiều widget.

Đề xuất tên Deutsch Lernen; người dùng đổi được. Theme nền kem #F7F5EF, chữ #182B29, xanh #14695D, vàng #D6A64A. Kiểm tra tương phản màu thực tế; màu gợi ý mạo từ phải kèm chữ der/die/das. Font hệ thống/local hỗ trợ Việt/Đức, body 16px trở lên, chiều rộng nội dung đọc vừa phải, spacing hệ 8px, radius 12–16px.

Desktop có sidebar, header gọn, khu học chính rộng; mobile có navigation thu gọn và các nút chạm dễ dùng. Trang vocabulary ưu tiên hình, từ và hành động học; màn học có thanh tiến độ, player và phản hồi rõ; analytics có insight thực tế. Không dùng hiệu ứng làm người học mất tập trung.

Có loading/empty/error/success, focus hiển thị, điều hướng bàn phím, label cho form, semantic HTML, không dựa màu để báo đáp án. Tôn trọng prefers-reduced-motion. Không phát audio tự động khi mở trang. Micro-animation 150–250ms, không gây lag trên máy đích.

Thiết kế ít nhất 8 màn thực: dashboard, curriculum, image vocabulary, flashcard/review, lesson, listening, practice result, library/settings. Kiểm tra ít nhất desktop 1366×768 và mobile 390×844. Screenshot từng màn; sửa overflow, nội dung cắt, chữ nhỏ, spacing lệch trước bàn giao.

## 8. Kiến trúc và dữ liệu

Cấu trúc đề xuất:

```text
project/
  app/                  # app factory, blueprints, services, templates
  app/static/           # CSS, JS, icons/fonts cục bộ
  content/              # curriculum, bài/từ/câu hỏi được duyệt, manifests
  assets/               # PDF, audio, image crops/thumbs
  instance/             # SQLite, ghi âm, backup; không commit dữ liệu cá nhân
  tools/                # nhập, OCR, crop, validate, báo cáo coverage
  tests/                # test logic và browser
  requirements.txt
  migrations/
  start.bat
  setup_windows.bat
  README_VI.md
  CONTENT_COVERAGE.md
  THIRD_PARTY_NOTICES.md
```

Tách metadata/nội dung khỏi tiến độ. Các bảng: profiles; assets; modules; lessons; activities; activity_sources; vocabulary; vocabulary_senses; images; image_regions; audio_links; srs_cards; review_events; attempts; study_sessions; skill_assessments; recordings; exam_forms; exam_attempts; import_jobs. Có foreign keys, migration, index và unique key cho importer.

Mỗi source_reference có asset_id, pdf_page 1-based, printed_page nếu xác định, exercise_id. Mỗi audio_link có source file, start/end seconds, book_track nếu xác minh và người/thời điểm duyệt. Mỗi hoạt động có level, skill, prompt, câu trả lời/rubric, hints, explanation, source, status.

Workflow nội dung: imported → extracted/OCR → classified → draft → reviewed → published. Bài có lỗi OCR/ảnh lộ đáp án/audio chưa khớp không được published. Không tự đổi tất cả sang reviewed chỉ vì chạy importer thành công. Có màn/báo cáo hàng đợi rà soát, không giấu nội dung thiếu.

Tiến độ phân biệt completion, mastery và attendance. Điểm có score_kind automatic/human/self. Timestamp UTC, lịch/ngày học theo Asia/Ho_Chi_Minh. Restore và migration có backup trước khi ghi; SQLite transaction; SQL tham số hóa. Đường dẫn tài nguyên validate, không cho mở tùy ý file ngoài assets; giới hạn upload và phục vụ MIME phù hợp. Nội dung nhập không render HTML tùy ý chưa sanitize.

## 9. Quy trình triển khai và tiêu chí nội dung

Bước 1: kiểm tra repo/AGENTS.md/môi trường và attachments, lập inventory/dedupe/gap report. Nếu đã có code, giữ thay đổi của người dùng, mở rộng có kiểm soát, không reset toàn bộ.

Bước 2: xây skeleton chạy thật, database, importer và design system. Thư viện PDF/MP3 dùng ngay. Lưu roadmap nhưng tiếp tục viết code trong cùng nhiệm vụ.

Bước 3: tạo một lát chức năng đầy đủ cho chủ đề đồ vật/nhà ở: ít nhất 20 từ đã kiểm tra, 12 từ có hình phù hợp, 3 dạng bài hình ảnh, một bài đọc, một bài viết, SRS và lưu kết quả. Đây là mốc nghiệm thu pilot để phát hiện lỗi pipeline, không phải giới hạn cuối dự án. Nếu sách không đủ hình tách hợp lệ, dùng minh họa tự biên soạn dễ hiểu và ghi nguồn, không nhét ảnh trang nguyên chứa đáp án.

Bước 4: mở rộng các phân hệ và chủ đề theo lộ trình. Ưu tiên từ A1 thường gặp, bài nghe đã map, đọc–viết nguồn thật. Phải phát hành đủ nội dung pilot và kế hoạch/coverage toàn chương trình; tiếp tục số hóa nguồn thực tế trong phạm vi khả thi của phiên, không tuyên bố 96 bài hoàn chỉnh khi chưa đạt. Mỗi module published cần đầu ra và đủ bốn kỹ năng; kỹ năng thiếu ghi rõ.

Bước 5: kiểm thử, sửa lỗi, chạy browser và kiểm tra giao diện, đóng gói và hướng dẫn. Tránh phụ thuộc vào Internet ở runtime. Không cần người dùng duyệt lại các thao tác cục bộ có thể đảo ngược đã được giao. Chỉ hỏi nếu thiếu thông tin quyết định kiến trúc mà không thể suy ra, thao tác phá hủy hoặc bị chặn quyền; tiếp tục việc độc lập trong khi chờ.

## 10. Kiểm thử và điều kiện hoàn thành

- Asset hash chính xác; import hai lần không nhân đôi; phát hiện PDF gần trùng; filenames UTF-8/space không gây lỗi.
- Chấm bài có umlaut/ß đúng chính sách: tùy bài cho phép ae/oe/ue hay báo lỗi; không tự coi ß=ss cho mọi trường hợp. Chấm danh từ viết hoa: phản hồi chính tả và chính sách điểm rõ.
- Crop kiểm tra không có từ đáp án, hotspot responsive đúng, cùng lemma khác nghĩa không bị trộn.
- SRS due dates/Again/Hard/Good/Easy có test thực; thời gian/múi giờ, tồn đọng, reset không làm mất tiến độ ngoài ý muốn.
- Lưu tiến độ qua restart, hồ sơ không trộn dữ liệu, backup/restore gồm DB và recordings và không mất tài nguyên.
- Player phát MP3 thật; không thể phát thiếu vẫn hiển thị trạng thái hữu ích. Microphone denial không crash. Browser/codec không hỗ trợ có fallback tải bản ghi.
- Bài viết/nói chưa chấm không xuất tổng điểm “đạt A1”. Không có phần thi nguồn thiếu bị hiển thị hoàn thành.
- Pytest cho importer, chấm đáp án, SRS và persistence; Playwright hoặc công cụ tương đương cho luồng học, trả lời, lưu, review, audio, responsive và keyboard.
- Chặn tất cả request ngoài localhost khi kiểm thử browser, duyệt network log. Khi chặn mạng, toàn bộ chức năng đã hoàn thành vẫn chạy. Không chỉ kiểm tra home page rồi kết luận offline.
- Kiểm tra launcher/cài trên Windows riêng; nếu môi trường hiện tại không có Windows, bàn giao script và checklist nhưng báo chưa kiểm chứng trên Windows.

## 11. Bàn giao cuối

Cung cấp toàn bộ source, dữ liệu nội dung được duyệt, asset manifest, report tài nguyên thiếu/không khớp, requirements khóa phiên bản, script cài/khởi chạy Windows, hướng dẫn Việt, test report, screenshots và backup instructions. Chuẩn bị wheelhouse cài offline khi thực tế tải/build được; nếu chưa làm được, ghi yêu cầu chuẩn bị thay vì hứa không cần mạng từ lần cài đầu.

Nếu đóng ZIP hãy include code và tài nguyên cần cho sử dụng cá nhân, bỏ môi trường ảo/cache/dữ liệu nhạy cảm. Có README cách cài, chạy, dừng server, khắc phục port bị chiếm, thêm tài liệu và phục hồi.

Báo cáo cuối phải ghi rõ:
1. Những luồng đã chạy được và cách mở ứng dụng.
2. Số module/bài/từ/hình/audio đã published, draft, unmapped.
3. Kiểm thử đã qua và những kiểm thử chưa thực hiện.
4. Phần thiếu nội dung hoặc cần rà soát ngôn ngữ; không giấu giới hạn sau câu “hoàn thành”.

**Bắt đầu thực hiện ngay:** kiểm tra tài nguyên và dự án, rồi viết code ứng dụng chạy được. Dùng các quyết định mặc định trên nếu không có yêu cầu khác. Mục tiêu là website học tập thực dụng có thiết kế chỉnh chu, học qua ảnh gắn với ôn truy hồi, nội dung truy xuất được nguồn và tiến độ thật.
