<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ôn Tập Lịch Sử Đảng</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
            background-color: #f4f4f4;
            color: #333;
        }
        .quiz-container {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .question-block {
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        .question-block:last-child {
            border-bottom: none;
        }
        .question-text {
            font-weight: bold;
            margin-bottom: 10px;
        }
        .options label {
            display: block;
            margin-bottom: 8px;
            cursor: pointer;
            padding: 5px;
            border-radius: 4px;
        }
        .options label:hover {
            background-color: #e9e9e9;
        }
        .options input[type="radio"] {
            margin-right: 10px;
        }
        .correct-answer {
            background-color: #d4edda !important; /* Light green for correct */
            color: #155724;
            font-weight: bold;
        }
        .selected-incorrect {
            background-color: #f8d7da; /* Light red for incorrect selection */
            color: #721c24;
        }
        .controls {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #ccc;
        }
        .controls button {
            padding: 10px 15px;
            margin-right: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        .controls button:hover {
            background-color: #0056b3;
        }
        #score-container {
            margin-top: 20px;
            font-weight: bold;
            font-size: 18px;
        }
        .hidden {
            display: none;
        }
        .source-cite {
            font-size: 0.8em;
            color: #555;
            margin-left: 5px;
        }
    </style>
</head>
<body>

<div class="quiz-container">
    <h1>Bài Ôn Tập Trắc Nghiệm Lịch Sử Đảng Cộng Sản Việt Nam</h1>
    <div id="quiz-form">
        </div>

    <div class="controls">
        <button onclick="submitQuiz()">Nộp Bài / Xem Điểm</button>
        <button id="toggle-answers-btn" onclick="toggleAnswers()">Hiện Đáp Án</button>
        <button onclick="resetQuiz()">Làm Lại</button>
    </div>

    <div id="score-container"></div>
</div>

<script>
    const questions = [
        {
            id: 1,
            question: "Đâu là một trong những yếu tố quốc tế tác động đến bối cảnh ra đời của Đảng Cộng sản Việt Nam?",
            options: [
                "Chiến tranh thế giới thứ nhất bùng nổ.",
                "Sự ra đời của Quốc tế cộng sản (3/1919).",
                "Cách mạng Tân Hợi ở Trung Quốc.",
                "Sự thành lập của Liên Hợp Quốc."
            ],
            correctAnswer: 1,
            source: 2
        },
        {
            id: 2,
            question: "Sự kiện nào đánh dấu Việt Nam chính thức trở thành thuộc địa của Pháp?",
            options: [
                "Pháp tấn công Đà Nẵng (1/9/1858).",
                "Hiệp ước Patơnốt được ký kết (6/6/1884).",
                "Phong trào Cần Vương thất bại.",
                "Phan Bội Châu xuất dương sang Nhật."
            ],
            correctAnswer: 1,
            source: 3
        },
        {
            id: 3,
            question: "Mâu thuẫn chủ yếu trong xã hội Việt Nam dưới ách thống trị của thực dân Pháp là gì?",
            options: [
                "Giai cấp tư sản và giai cấp vô sản.",
                "Địa chủ phong kiến và nông dân.",
                "Dân tộc Việt Nam với đế quốc xâm lược và nông dân Việt Nam với địa chủ phong kiến.",
                "Triều đình nhà Nguyễn với các thế lực ngoại xâm."
            ],
            correctAnswer: 2,
            source: 5
        },
        {
            id: 4,
            question: "Phong trào yêu nước nào sau đây theo khuynh hướng tư sản?",
            options: [
                "Khởi nghĩa Yên Thế.",
                "Phong trào Cần Vương.",
                "Phong trào Đông Du của Phan Bội Châu.",
                "Phong trào Xô Viết Nghệ Tĩnh."
            ],
            correctAnswer: 2,
            source: 5 // Assuming this refers to the section "Các phong trào yêu nước theo khuynh hướng phong kiến và tư sản"
        },
        {
            id: 5,
            question: "Nguyên nhân chính dẫn đến sự thất bại của các phong trào yêu nước theo khuynh hướng phong kiến và tư sản là gì?",
            options: [
                "Thiếu sự ủng hộ của quần chúng nhân dân.",
                "Sự đàn áp tàn bạo của thực dân Pháp.",
                "Đường lối chưa đáp ứng được yêu cầu thực tiễn cách mạng.",
                "Mâu thuẫn nội bộ trong các phong trào."
            ],
            correctAnswer: 2,
            source: 5
        },
        {
            id: 6,
            question: "Sự kiện nào đánh dấu bước chuyển từ đấu tranh tự phát sang tự giác của phong trào công nhân Việt Nam?",
            options: [
                "Nguyễn Ái Quốc đọc Sơ thảo lần thứ nhất những luận cương về vấn đề dân tộc và vấn đề thuộc địa của Lênin (7/1920).",
                "Thành lập Hội Việt Nam Cách mạng Thanh niên (6/1925).",
                "Chi bộ Cộng sản đầu tiên được thành lập ở Hà Nội (3/1929).",
                "Sự ra đời của ba tổ chức cộng sản (1929)."
            ],
            correctAnswer: 1, // "Tự phát <- 1925 -> Tự giác" implies 1925 is the turning point.
            source: 6
        },
        {
            id: 7,
            question: "Hội nghị thành lập Đảng Cộng sản Việt Nam diễn ra vào thời gian và địa điểm nào?",
            options: [
                "Từ ngày 6/1 đến 7/2/1930, tại Hương Cảng, Trung Quốc.",
                "Tháng 3/1929, tại Hà Nội, Việt Nam.",
                "Tháng 6/1925, tại Quảng Châu, Trung Quốc.",
                "Tháng 10/1930, tại Sài Gòn, Việt Nam."
            ],
            correctAnswer: 0,
            source: 7 // Assuming 7 covers the time and place details of the conference.
        },
        {
            id: 8,
            question: "Ý nghĩa nào sau đây KHÔNG phải là ý nghĩa lịch sử của việc thành lập Đảng Cộng sản Việt Nam?",
            options: [
                "Chấm dứt cuộc khủng hoảng về đường lối cứu nước và giai cấp lãnh đạo.",
                "Cách mạng Việt Nam trở thành một bộ phận của cách mạng thế giới.",
                "Làm cho Việt Nam ngay lập tức trở thành một nước xã hội chủ nghĩa.",
                "Tạo cơ sở cho những bước nhảy vọt của cách mạng Việt Nam."
            ],
            correctAnswer: 2,
            source: 7 // Source 7 has "Ý nghĩa lịch sử của thành lập ĐCSVN"
        },
        {
            id: 9,
            question: "Nội dung nào là điểm khác biệt cơ bản giữa Cương lĩnh chính trị đầu tiên (2/1930) và Luận cương chính trị (10/1930) về nhiệm vụ cách mạng?",
            options: [
                "Cương lĩnh đặt nhiệm vụ đánh đổ đế quốc Pháp lên hàng đầu, sau đó mới đến phong kiến; Luận cương đặt nhiệm vụ đánh đổ phong kiến lên hàng đầu, sau đó mới đến đế quốc Pháp.",
                "Cương lĩnh đặt nhiệm vụ đánh đổ phong kiến lên hàng đầu; Luận cương đặt nhiệm vụ đánh đổ đế quốc Pháp lên hàng đầu.",
                "Cả hai đều đặt nhiệm vụ đánh đổ đế quốc Pháp lên hàng đầu.",
                "Cả hai đều đặt nhiệm vụ đánh đổ phong kiến lên hàng đầu."
            ],
            correctAnswer: 0,
            source: 9
        },
        {
            id: 10,
            question: "Trong giai đoạn phong trào dân chủ 1936 – 1939, kẻ thù trước mắt được Đảng Cộng sản Đông Dương xác định là gì?",
            options: [
                "Chủ nghĩa phát xít nói chung.",
                "Bọn phản động thuộc địa và bè lũ tay sai.",
                "Toàn bộ đế quốc Pháp.",
                "Giai cấp địa chủ phong kiến."
            ],
            correctAnswer: 1,
            source: 13 // "Hội nghị BCH TW Đảng CS Đông Dương 7/1936 + Kẻ thù: Bọn phản động thuộc địa và bè lũ tay sai"
        },
        {
            id: 11,
            question: "Hội nghị Ban Chấp hành Trung ương Đảng Cộng sản Đông Dương tháng 11/1939 đã chủ trương thành lập mặt trận nào?",
            options: [
                "Mặt trận Việt Minh.",
                "Mặt trận Thống nhất nhân dân phản đế Đông Dương.",
                "Mặt trận Thống nhất dân tộc phản đế Đông Dương.",
                "Mặt trận Liên Việt."
            ],
            correctAnswer: 2,
            source: 18
        },
        {
            id: 12,
            question: "Hội nghị lần thứ tám Ban Chấp hành Trung ương Đảng khóa I (5/1941) đã quyết định thành lập mặt trận nào?",
            options: [
                "Mặt trận Thống nhất dân tộc phản đế Đông Dương.",
                "Mặt trận Việt Minh.",
                "Mặt trận Dân chủ Đông Dương.",
                "Mặt trận Liên Việt."
            ],
            correctAnswer: 1,
            source: 20
        },
        {
            id: 13,
            question: "Chỉ thị “Nhật – Pháp bắn nhau và hành động của chúng ta” (12/3/1945) đã xác định khẩu hiệu đấu tranh là gì?",
            options: [
                "“Đánh đuổi phát xít Nhật – Pháp”.",
                "“Đánh đuổi phát xít Nhật”.",
                "“Chống đế quốc và phong kiến”.",
                "“Ruộng đất cho dân cày”."
            ],
            correctAnswer: 1,
            source: 23
        },
        {
            id: 14,
            question: "Lệnh tổng khởi nghĩa trên toàn quốc được Hội nghị toàn quốc của Đảng quyết định phát vào thời điểm nào?",
            options: [
                "Ngày 12/8/1945.",
                "Ngày 13/8/1945.",
                "Ngày 14-15/8/1945.",
                "Ngày 19/8/1945."
            ],
            correctAnswer: 2,
            source: 27
        },
        {
            id: 15,
            question: "Nguyên nhân nào được xem là quyết định nhất đưa Cách mạng Tháng Tám 1945 giành thắng lợi?",
            options: [
                "Thời cơ khách quan thuận lợi.",
                "Sự lãnh đạo của Đảng Cộng sản Đông Dương.",
                "Sự nổi dậy đồng loạt của quần chúng nhân dân.",
                "Sự suy yếu của phát xít Nhật."
            ],
            correctAnswer: 1,
            source: 34
        },
        {
            id: 16,
            question: "Sau Cách mạng Tháng Tám 1945, khó khăn lớn nhất mà nước ta phải đối mặt là gì?",
            options: [
                "Nạn đói và nạn dốt.",
                "Ngân quỹ quốc gia trống rỗng.",
                "Giặc ngoại xâm và nội phản.", // Document says "Giặc ngoại xâm ( vđ lớn nhất )"
                "Kinh nghiệm quản lý đất nước còn non yếu."
            ],
            correctAnswer: 2,
            source: 44
        },
        {
            id: 17,
            question: "Chỉ thị “Kháng chiến kiến quốc” (25/11/1945) xác định kẻ thù chính của cách mạng Việt Nam là ai?",
            options: [
                "Quân Tưởng Giới Thạch.",
                "Thực dân Pháp.",
                "Đế quốc Anh.",
                "Phát xít Nhật còn sót lại."
            ],
            correctAnswer: 1,
            source: 45
        },
        {
            id: 18,
            question: "Chính sách đối ngoại của Đảng và Chính phủ ta giai đoạn 1945-1946 là gì?",
            options: [
                "Kiên quyết chống lại tất cả các thế lực ngoại xâm.",
                "“Thêm bạn bớt thù”, nhân nhượng có nguyên tắc với Tưởng và Pháp.",
                "Chỉ hòa hoãn với Pháp, kiên quyết chống Tưởng.",
                "Dựa hẳn vào một cường quốc để chống lại các thế lực khác."
            ],
            correctAnswer: 1,
            source: 47 // Source 47 covers "Chính sách đối ngoại"
        },
        {
            id: 19,
            question: "Sự kiện nào trực tiếp dẫn đến việc Đảng ta phát động toàn quốc kháng chiến chống thực dân Pháp?",
            options: [
                "Pháp tăng cường khiêu khích và lấn chiếm Hải Phòng, Hà Nội.",
                "Pháp gửi tối hậu thư đòi Việt Nam đầu hàng (18/12/1946).",
                "Hồ Chủ tịch ra Lời kêu gọi “Toàn quốc kháng chiến”.",
                "Ban Thường vụ Trung ương ra chỉ thị “Toàn dân kháng chiến”."
            ],
            correctAnswer: 1,
            source: 49 // Refers to the events leading to 19/12/1946
        },
        {
            id: 20,
            question: "Đường lối kháng chiến chống thực dân Pháp của Đảng ta KHÔNG có tính chất nào sau đây?",
            options: [
                "Toàn dân.",
                "Toàn diện.",
                "Lâu dài.",
                "Đánh nhanh thắng nhanh."
            ],
            correctAnswer: 3,
            source: 50 // Source 50 lists "toàn dân, toàn diện, lâu dài"
        },
        {
            id: 21,
            question: "Đại hội đại biểu toàn quốc lần thứ II của Đảng (2/1951) quyết định đổi tên Đảng thành gì?",
            options: [
                "Đảng Cộng sản Việt Nam.",
                "Đảng Lao động Việt Nam.",
                "Đảng Cộng sản Đông Dương.",
                "Hội Nghiên cứu Chủ nghĩa Mác ở Đông Dương."
            ],
            correctAnswer: 1,
            source: 51 // "Thành lập Đảng riêng ở VN: Đảng Lao động VN"
        },
        {
            id: 22,
            question: "Chiến thắng nào của quân và dân ta đã giành được quyền chủ động chiến lược trên chiến trường Bắc Bộ trong kháng chiến chống Pháp?",
            options: [
                "Chiến dịch Việt Bắc Thu – Đông 1947.",
                "Chiến dịch Biên giới Thu – Đông 1950.",
                "Chiến dịch Hòa Bình Đông – Xuân 1951-1952.",
                "Chiến dịch Điện Biên Phủ 1954."
            ],
            correctAnswer: 1,
            source: 54
        },
        {
            id: 23,
            question: "Nội dung nào sau đây KHÔNG phải là điều khoản của Hiệp định Giơ-ne-vơ (1954) về Đông Dương?",
            options: [
                "Đình chỉ chiến sự ở Việt Nam.",
                "Tạm thời chia cắt đất nước Việt Nam ở vĩ tuyến 17.",
                "Pháp phải rút quân hoàn toàn ra khỏi Đông Dương.",
                "Mỹ được phép đưa quân vào miền Nam Việt Nam để thay thế Pháp."
            ],
            correctAnswer: 3, // Source 60 indicates US did not sign.
            source: 58 // and surrounding content about the agreement
        },
        {
            id: 24,
            question: "Chiến lược chiến tranh nào của Mỹ ở miền Nam Việt Nam có đặc trưng là \"dùng người Việt đánh người Việt\"?",
            options: [
                "Chiến tranh đơn phương (1954-1960).",
                "Chiến tranh đặc biệt (1961-1965).",
                "Chiến tranh cục bộ (1965-1968).",
                "Việt Nam hóa chiến tranh (1969-1975)."
            ],
            correctAnswer: 0,
            source: 65 // "Dùng người Việt đánh người Việt ( chính quyền Ngô Đình Diệm )"
        },
        {
            id: 25,
            question: "Đại hội đại biểu toàn quốc lần thứ III của Đảng (9/1960) xác định vai trò của cách mạng miền Nam là gì?",
            options: [
                "Giữ vai trò quyết định trực tiếp đối với sự nghiệp giải phóng miền Nam.",
                "Xây dựng tiềm lực và bảo vệ căn cứ địa của cả nước.",
                "Có vai trò hậu phương lớn, chi viện cho tiền tuyến lớn.",
                "Thực hiện cải cách ruộng đất và xây dựng chủ nghĩa xã hội."
            ],
            correctAnswer: 0,
            source: 71 // "miền Nam giữ vai trò quyết định giải phóng."
        },
        {
            id: 26,
            question: "Sự kiện nào được Mỹ dựng lên để lấy cớ leo thang chiến tranh, ném bom phá hoại miền Bắc Việt Nam?",
            options: [
                "Phong trào Đồng khởi ở miền Nam (1959-1960).",
                "Sự kiện Vịnh Bắc Bộ (5/8/1964).",
                "Cuộc Tổng tiến công và nổi dậy Tết Mậu Thân (1968).",
                "Chiến thắng Đường 9 – Khe Sanh (1968)."
            ],
            correctAnswer: 1,
            source: 77
        },
        {
            id: 27,
            question: "Thắng lợi nào của quân dân ta được coi là \"Điện Biên Phủ trên không\"?",
            options: [
                "Đánh bại cuộc hành quân Gianxơn Xiti của Mỹ (1967).",
                "Đánh bại cuộc tập kích chiến lược bằng máy bay B-52 của Mỹ vào Hà Nội, Hải Phòng cuối năm 1972.",
                "Chiến dịch phòng không bảo vệ Hà Nội năm 1966.",
                "Bắn rơi nhiều máy bay Mỹ trong chiến tranh phá hoại lần thứ nhất."
            ],
            correctAnswer: 1,
            source: 81 // also 82
        },
        {
            id: 28,
            question: "Hiệp định Paris về chấm dứt chiến tranh, lập lại hòa bình ở Việt Nam được ký kết vào ngày tháng năm nào?",
            options: [
                "20/7/1954.",
                "27/01/1973.",
                "30/4/1975.",
                "02/7/1976."
            ],
            correctAnswer: 1,
            source: 83
        },
        {
            id: 29,
            question: "Phong trào Đồng khởi (1959-1960) ở miền Nam đã làm phá vỡ chiến lược chiến tranh nào của Mỹ?",
            options: [
                "Chiến tranh đơn phương.",
                "Chiến tranh đặc biệt.",
                "Chiến tranh cục bộ.",
                "Việt Nam hóa chiến tranh."
            ],
            correctAnswer: 0,
            source: 85
        },
        {
            id: 30,
            question: "Những thắng lợi quân sự nào đã làm phá sản về cơ bản chiến lược \"Chiến tranh đặc biệt\" của Mỹ ở miền Nam?",
            options: [
                "Ấp Bắc, Vạn Tường.",
                "Bình Giã, An Lão, Ba Gia, Đồng Xoài.",
                "Chiến dịch Tây Nguyên, Huế - Đà Nẵng.",
                "Điện Biên Phủ trên không."
            ],
            correctAnswer: 1,
            source: 87 // also 88
        },
        {
            id: 31,
            question: "Hội nghị hiệp thương chính trị thống nhất đất nước về mặt nhà nước được tổ chức vào thời gian nào và ở đâu?",
            options: [
                "Tháng 6/1976, tại Hà Nội.",
                "Ngày 15 – 21/11/1975, tại Sài Gòn.",
                "Ngày 25/4/1976, trên cả nước.",
                "Ngày 3/7/1976, tại Hà Nội."
            ],
            correctAnswer: 1,
            source: 90
        },
        {
            id: 32,
            question: "Kỳ họp thứ nhất Quốc hội thống nhất (khóa VI) đã quyết định tên nước là gì?",
            options: [
                "Việt Nam Dân chủ Cộng hòa.",
                "Cộng hòa Xã hội chủ nghĩa Việt Nam.",
                "Cộng hòa Miền Nam Việt Nam.",
                "Liên bang Đông Dương."
            ],
            correctAnswer: 1,
            source: 91
        },
        {
            id: 33,
            question: "Thành phố Sài Gòn được đổi tên thành Thành phố Hồ Chí Minh tại sự kiện nào?",
            options: [
                "Hội nghị hiệp thương chính trị (11/1975).",
                "Cuộc tổng tuyển cử bầu Quốc hội chung (25/4/1976).",
                "Kỳ họp thứ nhất Quốc hội thống nhất (24/6 – 3/7/1976).",
                "Đại hội Đảng toàn quốc lần thứ IV (12/1976)."
            ],
            correctAnswer: 2,
            source: 94
        },
        {
            id: 34,
            question: "Đặc trưng của chủ trương công nghiệp hóa trước thời kỳ đổi mới (trước Đại hội VI) là gì?",
            options: [
                "Ưu tiên phát triển công nghiệp nhẹ.",
                "Phát triển đồng đều công nghiệp nặng và công nghiệp nhẹ.",
                "Ưu tiên phát triển công nghiệp nặng.",
                "Lấy nông nghiệp làm mặt trận hàng đầu."
            ],
            correctAnswer: 2,
            source: 97 // "Đặc trưng CNH trước đổi mới là Phát triển CN nặng"
        },
        {
            id: 35,
            question: "Đại hội nào của Đảng lần đầu tiên đề cập đến công nghiệp hóa xã hội chủ nghĩa?",
            options: [
                "Đại hội II (2/1951).",
                "Đại hội III (9/1960).",
                "Đại hội IV (12/1976).",
                "Đại hội V (3/1982)."
            ],
            correctAnswer: 1,
            source: 97 // "Đại hội III (9/1960): đề cập đến CNH"
        },
        {
            id: 36,
            question: "Đại hội V (3/1982) của Đảng đã có chủ trương đúng đắn nào về công nghiệp hóa?",
            options: [
                "Tiếp tục ưu tiên phát triển công nghiệp nặng.",
                "Lấy nông nghiệp làm mặt trận hàng đầu, phát triển công nghiệp nhẹ song song với công nghiệp nặng.",
                "Chuyển sang nền kinh tế thị trường.",
                "Chỉ tập trung phát triển công nghiệp địa phương."
            ],
            correctAnswer: 1,
            source: 102
        },
        {
            id: 37,
            question: "Một trong những hạn chế của chủ trương công nghiệp hóa trước đổi mới là gì?",
            options: [
                "Công nghiệp hóa theo mô hình kinh tế mở, hướng ngoại.",
                "Quá coi trọng vai trò của nông nghiệp.",
                "Công nghiệp hóa theo mô hình nền kinh tế khép kín, hướng nội, thiên về công nghiệp nặng.",
                "Áp dụng cơ chế kinh tế thị trường quá sớm."
            ],
            correctAnswer: 2,
            source: 103
        },
        {
            id: 38,
            question: "Đại hội nào của Đảng mở đầu cho công cuộc đổi mới toàn diện đất nước, chuyển từ kinh tế kế hoạch tập trung sang kinh tế thị trường định hướng xã hội chủ nghĩa?",
            options: [
                "Đại hội V (3/1982).",
                "Đại hội VI (12/1986).",
                "Đại hội VII (6/1991).",
                "Đại hội VIII (6/1996)."
            ],
            correctAnswer: 1,
            source: 108 // "Đổi mới toàn diện kinh tế, chuyển từ nền kinh tế kế hoạch tập trung bao cấp sang cơ chế kinh tế thị trường định hướng xã hội chủ nghĩa." under Đại hội VI
        },
        {
            id: 39,
            question: "Đâu KHÔNG phải là đặc trưng của cơ chế kinh tế kế hoạch hóa tập trung, quan liêu, bao cấp?",
            options: [
                "Kinh tế do Nhà nước quản lý tập trung, kế hoạch hóa toàn diện.",
                "Khuyến khích cạnh tranh và sự năng động của các thành phần kinh tế.",
                "Tổ chức quan liêu, nhiều bộ phận chồng chéo, thiếu linh hoạt.",
                "Bao cấp, trợ cấp nhiều, thiếu cơ chế thị trường."
            ],
            correctAnswer: 1,
            source: 111 // Sources 111-113 describe the characteristics, this one is the opposite.
        },
        {
            id: 40,
            question: "Mô hình kinh tế tổng quát của Việt Nam trong thời kỳ quá độ lên chủ nghĩa xã hội, được khẳng định từ Đại hội IX đến Đại hội XIII, là gì?",
            options: [
                "Kinh tế kế hoạch hóa tập trung.",
                "Kinh tế thị trường tự do.",
                "Kinh tế thị trường định hướng xã hội chủ nghĩa.",
                "Kinh tế hàng hóa nhiều thành phần có sự quản lý của nhà nước."
            ],
            correctAnswer: 2,
            source: 125
        }
    ];

    const quizForm = document.getElementById('quiz-form');
    const scoreContainer = document.getElementById('score-container');
    const toggleAnswersBtn = document.getElementById('toggle-answers-btn');
    let answersVisible = false;

    function renderQuestions() {
        quizForm.innerHTML = ''; // Clear existing questions
        questions.forEach((q, index) => {
            const questionBlock = document.createElement('div');
            questionBlock.classList.add('question-block');
            questionBlock.id = `question-${q.id}`;

            const questionText = document.createElement('div');
            questionText.classList.add('question-text');
            questionText.innerHTML = `${index + 1}. ${q.question} <span class="source-cite">[Nguồn: ${q.source}]</span>`;
            questionBlock.appendChild(questionText);

            const optionsDiv = document.createElement('div');
            optionsDiv.classList.add('options');
            q.options.forEach((option, i) => {
                const label = document.createElement('label');
                const radio = document.createElement('input');
                radio.type = 'radio';
                radio.name = `question${q.id}`;
                radio.value = i;
                label.appendChild(radio);
                label.appendChild(document.createTextNode(option));
                optionsDiv.appendChild(label);
            });
            questionBlock.appendChild(optionsDiv);
            quizForm.appendChild(questionBlock);
        });
    }

    function submitQuiz() {
        let score = 0;
        let answeredCount = 0;
        questions.forEach(q => {
            const selectedOption = document.querySelector(`input[name="question${q.id}"]:checked`);
            const questionBlock = document.getElementById(`question-${q.id}`);
            const optionLabels = questionBlock.querySelectorAll('.options label');

            // Clear previous highlights
            optionLabels.forEach(label => {
                label.classList.remove('correct-answer', 'selected-incorrect');
            });

            if (selectedOption) {
                answeredCount++;
                const userAnswer = parseInt(selectedOption.value);
                if (userAnswer === q.correctAnswer) {
                    score++;
                }
            }
        });

        scoreContainer.textContent = `Bạn đã trả lời ${answeredCount}/${questions.length} câu. Số câu đúng: ${score}/${questions.length}.`;
        if (answersVisible) { // If answers are already visible, re-apply highlights
            showAnswers();
        }
    }

    function showAnswers() {
        questions.forEach(q => {
            const questionBlock = document.getElementById(`question-${q.id}`);
            const optionLabels = questionBlock.querySelectorAll('.options label');
            const selectedOption = document.querySelector(`input[name="question${q.id}"]:checked`);

            optionLabels.forEach((label, i) => {
                label.classList.remove('correct-answer', 'selected-incorrect'); // Clear previous
                if (i === q.correctAnswer) {
                    label.classList.add('correct-answer');
                } else if (selectedOption && parseInt(selectedOption.value) === i) {
                    label.classList.add('selected-incorrect');
                }
            });
        });
    }

    function hideAnswers() {
        questions.forEach(q => {
            const questionBlock = document.getElementById(`question-${q.id}`);
            const optionLabels = questionBlock.querySelectorAll('.options label');
            optionLabels.forEach(label => {
                label.classList.remove('correct-answer', 'selected-incorrect');
            });
        });
    }

    function toggleAnswers() {
        answersVisible = !answersVisible;
        if (answersVisible) {
            showAnswers();
            toggleAnswersBtn.textContent = 'Ẩn Đáp Án';
        } else {
            hideAnswers();
            toggleAnswersBtn.textContent = 'Hiện Đáp Án';
             // Re-submit to show score without answer highlights if quiz was submitted
            if (scoreContainer.textContent !== '') {
                 submitQuiz(); // This will re-evaluate and remove highlights if answers are hidden
            }
        }
    }

    function resetQuiz() {
        questions.forEach(q => {
            const selectedOption = document.querySelector(`input[name="question${q.id}"]:checked`);
            if (selectedOption) {
                selectedOption.checked = false;
            }
        });
        scoreContainer.textContent = '';
        if (answersVisible) { // If answers were visible, toggle to hide them
            toggleAnswers();
        } else { // Otherwise, just ensure all highlights are gone
            hideAnswers();
        }
        // Scroll to top
        window.scrollTo(0, 0);
    }

    // Initial render of questions
    renderQuestions();
</script>

</body>
</html>
