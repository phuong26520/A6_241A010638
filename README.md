Lab A6 - Controls lựa chọn và ứng dụng tích hợp giao diện - Đăng ký học phần

Thông tin sinh viên: Nguyễn Hoài Phương - MSSV 241A010638 - Lớp LTTTBDD - Môn INT4211 Lập trình trên các thiết bị di động - Tuần 6. Package vn.edu.vhu.ltdd.a6controls, ngôn ngữ Java và XML, minSdk 24, template Empty Views Activity, theme Theme.Material3.DayNight.NoActionBar.

Mô tả ngắn gọn

App Đăng ký học phần gồm hai màn hình. Màn hình 1 là một biểu mẫu nằm trong ScrollView với đầy đủ các nhóm control của bài: hai EditText nhập họ tên và MSSV, một Spinner chọn học phần lấy dữ liệu từ res/values/arrays.xml qua ArrayAdapter, một RadioGroup hai RadioButton chọn hệ đào tạo, ba CheckBox chọn buổi học kèm một TextView đếm số buổi, hai MaterialSwitch cho nhận thông báo và chế độ tối, một ToggleButton cho chế độ ưu tiên, hai nút Xác nhận và Làm lại đặt cạnh nhau. Nút Xác nhận kiểm tra hợp lệ theo bốn trường hợp rồi dùng Intent tường minh chuyển sang ConfirmActivity, truyền toàn bộ dữ liệu đã gói thành một chuỗi tóm tắt. Màn hình 2 hiển thị đúng bảy dòng thông tin và có nút Quay lại chỉnh sửa gọi finish().

Cấu trúc thư mục chính

app/src/main/java/vn/edu/vhu/ltdd/a6controls/MainActivity.java là màn hình 1, chứa toàn bộ phần ánh xạ control, Spinner adapter, các listener, hàm demBuoi(), xacNhan() và lamLai()
app/src/main/java/vn/edu/vhu/ltdd/a6controls/ConfirmActivity.java là màn hình 2, nhận chuỗi tóm tắt qua getIntent().getStringExtra và hiển thị
app/src/main/res/layout/activity_main.xml là biểu mẫu bọc trong ScrollView
app/src/main/res/layout/activity_confirm.xml là màn hình xác nhận
app/src/main/res/values/arrays.xml chứa string-array mon_hoc cho Spinner
app/src/main/res/values/strings.xml chứa nhãn, hint, bốn chuỗi báo lỗi và chuỗi định dạng tom_tat_format
app/src/main/AndroidManifest.xml khai báo MainActivity là launcher và ConfirmActivity với exported false

Các chức năng đã hoàn thành theo thang điểm

Đủ năm loại control lựa chọn là EditText, Spinner, RadioGroup và RadioButton, CheckBox, MaterialSwitch và ToggleButton, bố cục thẳng hàng trong một LinearLayout dọc, toàn bộ bọc trong ScrollView nên cuộn được trên màn hình nhỏ. Spinner đổ dữ liệu từ arrays.xml bằng ArrayAdapter.createFromResource kết hợp setDropDownViewResource. Kiểm tra hợp lệ đủ bốn trường hợp theo đúng thứ tự: trống họ tên thì setError và requestFocus tại ô họ tên, MSSV không đủ mười ký tự thì setError và requestFocus tại ô MSSV, chưa chọn hệ đào tạo thì Toast nhắc và dừng, chưa tích buổi nào thì Toast nhắc và dừng. Truyền dữ liệu sang màn hình xác nhận đầy đủ bảy dòng dùng một chuỗi định dạng có sẵn trong strings.xml, khóa extras là hằng số EXTRA_TOM_TAT dùng chung cho hai activity. Đã chạy đủ tám kịch bản kiểm thử trên emulator và ghi kết quả vào báo cáo, kèm bảng đối chiếu với Lab F3 Flutter. Hai bài nâng cao NC2 và NC3 đã làm.

Bài nâng cao đã thực hiện

NC2 - Đếm số buổi đã chọn và hiện ngay dưới nhóm CheckBox. Khai báo một biến CompoundButton.OnCheckedChangeListener tên demBuoiListener và gán cho cả ba CheckBox cbSang, cbChieu, cbToi, mỗi lần bật hoặc tắt bất kỳ ô nào listener đều gọi lại hàm demBuoi(). Hàm này đếm số ô đang checked rồi đặt nội dung cho tvDemBuoi bằng chuỗi đã chọn có phần tử định dạng, ví dụ Đã chọn 2 buổi học. Gọi demBuoi() một lần ngay sau khi gán listener để màn hình khởi động hiển thị đúng giá trị 0. Cách làm này chỉ viết một lần cho ba control, không trùng code và không cần sửa từng onClick khi thêm buổi học mới.

NC3 - Switch Chế độ tối đổi nền màn hình ngay lập tức. Thêm MaterialSwitch swCheDoToi với nhãn Chế độ tối, trong listener của Switch gọi AppCompatDelegate.setDefaultNightMode với MODE_NIGHT_YES khi bật và MODE_NIGHT_NO khi tắt. Vì theme của project kế thừa Theme.Material3.DayNight và res/values-night/themes.xml có sẵn nên chỉ một dòng lệnh là toàn bộ màn hình đổi sang nền tối, cả ConfirmActivity cũng đổi theo. Nút Làm lại có thêm điều kiện tắt lại Switch nếu nó đang bật để ứng dụng trở về giao diện sáng mặc định.

Cách chạy và kiểm thử

Mở project A6_241A010638 trong Android Studio, chọn emulator hoặc điện thoại từ API 24 trở lên rồi bấm Run app. Build bằng lệnh .\gradlew.bat assembleDebug với JAVA_HOME trỏ tới JBR của Android Studio. Kiểm thử tám kịch bản theo thứ tự: để trống họ tên rồi bấm Xác nhận, nhập MSSV năm chữ số, không chọn hệ đào tạo, không tích buổi học, điền đủ rồi bấm Xác nhận, bấm Làm lại, xoay màn hình khi đang nhập dở, bấm Back từ màn hình xác nhận. Logcat lọc theo tag A6_241A010638 để xem học phần được chọn, hệ đào tạo và trạng thái hai Switch.

Ghi chú kỹ thuật

Dùng TextUtils.join thay cho String.join vì String.join cần API 26 trong khi minSdk của bài là 24. getCheckedRadioButtonId() trả về -1 khi chưa chọn nút nào nên đây là điều kiện kiểm tra của trường hợp 3. setError được xoá bằng setError(null) trong lamLai() vì setText rỗng không xoá icon lỗi. RadioGroup phải dùng clearCheck() vì nó không có giá trị mặc định để quay về, còn Spinner luôn có một phần tử được chọn nên phải dùng setSelection(0). onItemSelected chạy ngay khi setAdapter nên chỉ ghi Log.d, không dùng Toast để tránh thông báo lạ lúc mới mở app. Mọi control trong biểu mẫu đều có android:id nên trạng thái được hệ thống tự lưu và tự phục hồi khi xoay màn hình.
