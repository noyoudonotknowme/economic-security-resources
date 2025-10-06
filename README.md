<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Khung Nghiên cứu An ninh Kinh tế Việt Nam</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            padding: 20px;
            min-height: 100vh;
        }
        
        .header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
        }
        
        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .header p {
            font-size: 1.1em;
            opacity: 0.9;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.3);
        }
        
        .tree {
            padding: 20px;
        }
        
        .tree ul {
            position: relative;
            padding-top: 20px;
            list-style: none;
        }
        
        .tree li {
            position: relative;
            padding: 10px 5px 0 5px;
            list-style: none;
        }
        
        .tree ul ul::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            border-left: 2px solid #ccc;
            width: 0;
            height: 20px;
        }
        
        .tree li::before,
        .tree li::after {
            content: '';
            position: absolute;
            top: 0;
            right: 50%;
            border-top: 2px solid #ccc;
            width: 50%;
            height: 20px;
        }
        
        .tree li::after {
            right: auto;
            left: 50%;
            border-left: 2px solid #ccc;
        }
        
        .tree li:only-child::after,
        .tree li:only-child::before {
            display: none;
        }
        
        .tree li:first-child::before,
        .tree li:last-child::after {
            border: 0 none;
        }
        
        .tree li:last-child::before {
            border-right: 2px solid #ccc;
            border-radius: 0 5px 0 0;
        }
        
        .tree li:first-child::after {
            border-radius: 5px 0 0 0;
        }
        
        .node {
            display: inline-block;
            padding: 10px 15px;
            text-decoration: none;
            color: #333;
            border: 2px solid #2a5298;
            border-radius: 8px;
            position: relative;
            transition: all 0.3s ease;
            background: white;
            cursor: pointer;
            min-width: 200px;
            text-align: center;
        }
        
        .node:hover {
            background: #2a5298;
            color: white;
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(42, 82, 152, 0.4);
        }
        
        .node.root {
            background: #2a5298;
            color: white;
            font-weight: bold;
            font-size: 1.1em;
            padding: 15px 25px;
        }
        
        .node.category {
            background: #f0f4f8;
            border-color: #5a7ba6;
            font-weight: 600;
        }
        
        .node.category:hover {
            background: #5a7ba6;
        }
        
        .node.link {
            background: #fff;
            font-size: 0.9em;
        }
        
        .node.link:hover {
            background: #2a5298;
        }
        
        .node a {
            color: inherit;
            text-decoration: none;
        }
        
        .description {
            font-size: 0.85em;
            color: #666;
            margin-top: 5px;
            font-style: italic;
        }
        
        .node:hover .description {
            color: #e0e0e0;
        }
        
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.7);
            animation: fadeIn 0.3s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 30px;
            border-radius: 10px;
            width: 80%;
            max-width: 600px;
            box-shadow: 0 5px 30px rgba(0,0,0,0.5);
            animation: slideIn 0.3s;
        }
        
        @keyframes slideIn {
            from {
                transform: translateY(-50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
        
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
            line-height: 20px;
        }
        
        .close:hover {
            color: #000;
        }
        
        .modal h2 {
            color: #2a5298;
            margin-bottom: 15px;
        }
        
        .modal p {
            line-height: 1.6;
            margin-bottom: 15px;
        }
        
        .modal a {
            color: #2a5298;
            text-decoration: none;
            font-weight: 600;
        }
        
        .modal a:hover {
            text-decoration: underline;
        }
        
        .search-box {
            margin-bottom: 20px;
            text-align: center;
        }
        
        .search-box input {
            width: 100%;
            max-width: 500px;
            padding: 12px 20px;
            font-size: 16px;
            border: 2px solid #2a5298;
            border-radius: 25px;
            outline: none;
            transition: all 0.3s ease;
        }
        
        .search-box input:focus {
            box-shadow: 0 0 10px rgba(42, 82, 152, 0.3);
        }
        
        .highlight {
            background-color: yellow;
            animation: pulse 1s;
        }
        
        @keyframes pulse {
            0%, 100% { background-color: yellow; }
            50% { background-color: #ffeb3b; }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>🔍 Khung Nghiên cứu An ninh Kinh tế Việt Nam</h1>
        <p>Tổng hợp các nguồn tài liệu, văn bản pháp luật và dữ liệu thống kê phục vụ nghiên cứu</p>
    </div>
    
    <div class="container">
        <div class="search-box">
            <input type="text" id="searchInput" placeholder="🔎 Tìm kiếm tài liệu, cơ quan, chủ đề...">
        </div>
        
        <div class="tree">
            <ul>
                <li>
                    <div class="node root">
                        AN NINH KINH TẾ VIỆT NAM
                    </div>
                    <ul>
                        <!-- Văn bản pháp luật -->
                        <li>
                            <div class="node category">
                                📜 VĂN BẢN PHÁP LUẬT
                            </div>
                            <ul>
                                <li>
                                    <div class="node link" onclick="showModal('thuvienphapluat', 'Thư viện Pháp luật', 'Cơ sở dữ liệu văn bản pháp luật toàn diện của Việt Nam, bao gồm Luật, Nghị định, Thông tư và các văn bản quy phạm pháp luật khác.', 'https://thuvienphapluat.vn')">
                                        Thư viện Pháp luật
                                        <div class="description">Văn bản QPPL VN</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('congbao', 'Cổng Thông tin điện tử Chính phủ', 'Công bố chính thức các văn bản của Chính phủ, Thủ tướng Chính phủ và các Bộ, ngành.', 'http://vanban.chinhphu.vn')">
                                        Cổng TTĐT Chính phủ
                                        <div class="description">Văn bản Chính phủ</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('quochoi', 'Cổng Thông tin điện tử Quốc hội', 'Văn bản pháp luật do Quốc hội, Ủy ban Thường vụ Quốc hội ban hành.', 'https://quochoi.vn')">
                                        Cổng TTĐT Quốc hội
                                        <div class="description">Luật, Nghị quyết QH</div>
                                    </div>
                                </li>
                            </ul>
                        </li>
                        
                        <!-- Số liệu thống kê -->
                        <li>
                            <div class="node category">
                                📊 SỐ LIỆU THỐNG KÊ
                            </div>
                            <ul>
                                <li>
                                    <div class="node link" onclick="showModal('gso', 'Tổng cục Thống kê', 'Cơ quan chính thống về số liệu thống kê kinh tế - xã hội của Việt Nam. Dữ liệu về GDP, lạm phát, xuất nhập khẩu, đầu tư, lao động...', 'https://www.gso.gov.vn')">
                                        Tổng cục Thống kê
                                        <div class="description">Số liệu KT-XH VN</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('sbv', 'Ngân hàng Nhà nước VN', 'Số liệu về chính sách tiền tệ, tỷ giá, lãi suất, dự trữ ngoại hối, tín dụng ngân hàng.', 'https://www.sbv.gov.vn')">
                                        NHNN Việt Nam
                                        <div class="description">Số liệu tài chính, tiền tệ</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('mof', 'Bộ Tài chính', 'Thông tin về ngân sách nhà nước, thuế, nợ công, chứng khoán, dự toán và quyết toán ngân sách.', 'https://www.mof.gov.vn')">
                                        Bộ Tài chính
                                        <div class="description">Ngân sách, thuế, nợ công</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('moit', 'Bộ Công Thương', 'Số liệu về xuất nhập khẩu, thương mại, công nghiệp, năng lượng.', 'https://www.moit.gov.vn')">
                                        Bộ Công Thương
                                        <div class="description">Thương mại, XNK</div>
                                    </div>
                                </li>
                            </ul>
                        </li>
                        
                        <!-- Cơ quan quốc tế -->
                        <li>
                            <div class="node category">
                                🌍 TỔ CHỨC QUỐC TẾ
                            </div>
                            <ul>
                                <li>
                                    <div class="node link" onclick="showModal('worldbank', 'World Bank Data', 'Dữ liệu kinh tế toàn cầu và Việt Nam: GDP, đầu tư, nghèo đói, phát triển.', 'https://data.worldbank.org')">
                                        World Bank
                                        <div class="description">Dữ liệu phát triển</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('imf', 'IMF Data', 'Dữ liệu về tài chính quốc tế, cán cân thanh toán, nợ nước ngoài, dự trữ ngoại hối.', 'https://www.imf.org/en/Data')">
                                        IMF
                                        <div class="description">Tài chính quốc tế</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('adb', 'Asian Development Bank', 'Dữ liệu kinh tế châu Á, báo cáo phát triển, dự báo kinh tế khu vực.', 'https://www.adb.org/data')">
                                        ADB
                                        <div class="description">Kinh tế châu Á</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('wto', 'WTO Stats', 'Thống kê thương mại quốc tế, rào cản thuế quan, cam kết thương mại.', 'https://www.wto.org/english/res_e/statis_e/statis_e.htm')">
                                        WTO
                                        <div class="description">Thương mại quốc tế</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('unctad', 'UNCTAD Data', 'Dữ liệu về đầu tư nước ngoài (FDI), thương mại và phát triển.', 'https://unctad.org/statistics')">
                                        UNCTAD
                                        <div class="description">Đầu tư, phát triển</div>
                                    </div>
                                </li>
                            </ul>
                        </li>
                        
                        <!-- Tài liệu học thuật -->
                        <li>
                            <div class="node category">
                                📚 TÀI LIỆU HỌC THUẬT
                            </div>
                            <ul>
                                <li>
                                    <div class="node link" onclick="showModal('googlescholar', 'Google Scholar', 'Công cụ tìm kiếm bài báo khoa học, luận văn, sách học thuật từ nhiều nguồn.', 'https://scholar.google.com')">
                                        Google Scholar
                                        <div class="description">Tìm kiếm học thuật</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('researchgate', 'ResearchGate', 'Mạng xã hội học thuật, chia sẻ bài báo, kết nối với nhà nghiên cứu.', 'https://www.researchgate.net')">
                                        ResearchGate
                                        <div class="description">Mạng xã hội học thuật</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('ssrn', 'SSRN', 'Mạng nghiên cứu khoa học xã hội, chuyên về kinh tế, tài chính, quản trị.', 'https://www.ssrn.com')">
                                        SSRN
                                        <div class="description">Nghiên cứu KT-XH</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('jstor', 'JSTOR', 'Thư viện số các tạp chí học thuật, sách, nguồn chính (cần đăng ký).', 'https://www.jstor.org')">
                                        JSTOR
                                        <div class="description">Tạp chí học thuật</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('nber', 'NBER', 'Nghiên cứu kinh tế của National Bureau of Economic Research.', 'https://www.nber.org')">
                                        NBER
                                        <div class="description">Nghiên cứu kinh tế</div>
                                    </div>
                                </li>
                            </ul>
                        </li>
                        
                        <!-- Báo cáo & Phân tích -->
                        <li>
                            <div class="node category">
                                📈 BÁO CÁO & PHÂN TÍCH
                            </div>
                            <ul>
                                <li>
                                    <div class="node link" onclick="showModal('vepr', 'VEPR', 'Viện Nghiên cứu Kinh tế và Chính sách (ĐH Quốc gia HN) - báo cáo vĩ mô, dự báo kinh tế VN.', 'http://vepr.org.vn')">
                                        VEPR
                                        <div class="description">Nghiên cứu KT VN</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('ciem', 'CIEM', 'Viện Nghiên cứu Quản lý Kinh tế Trung ương - nghiên cứu chính sách kinh tế vĩ mô.', 'http://ciem.org.vn')">
                                        CIEM
                                        <div class="description">Quản lý KT TW</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('vcci', 'VCCI', 'Phòng Thương mại và Công nghiệp Việt Nam - báo cáo môi trường kinh doanh, năng lực cạnh tranh.', 'https://www.vcci.com.vn')">
                                        VCCI
                                        <div class="description">Môi trường KD</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('wef', 'WEF Reports', 'Diễn đàn Kinh tế Thế giới - báo cáo cạnh tranh toàn cầu, rủi ro toàn cầu.', 'https://www.weforum.org/reports')">
                                        WEF
                                        <div class="description">Cạnh tranh toàn cầu</div>
                                    </div>
                                </li>
                            </ul>
                        </li>
                        
                        <!-- Tin tức & Phân tích -->
                        <li>
                            <div class="node category">
                                📰 TIN TỨC & TRUYỀN THÔNG
                            </div>
                            <ul>
                                <li>
                                    <div class="node link" onclick="showModal('vneconomy', 'VnEconomy', 'Báo điện tử chuyên về kinh tế Việt Nam, phân tích thị trường, chính sách.', 'https://vneconomy.vn')">
                                        VnEconomy
                                        <div class="description">Tin tức KT VN</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('cafef', 'CafeF', 'Tin tức tài chính, chứng khoán, bất động sản, doanh nghiệp Việt Nam.', 'https://cafef.vn')">
                                        CafeF
                                        <div class="description">Tài chính, CK</div>
                                    </div>
                                </li>
                                <li>
                                    <div class="node link" onclick="showModal('vietstock', 'VietStock', 'Dữ liệu chứng khoán, tài chính doanh nghiệp niêm yết tại Việt Nam.', 'https://vietstock.vn')">
                                        VietStock
                                        <div class="description">Thị trường CK</div>
                                    </div>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
    
    <!-- Modal -->
    <div id="infoModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal()">&times;</span>
            <h2 id="modalTitle"></h2>
            <p id="modalDescription"></p>
            <p><strong>Truy cập:</strong> <a id="modalLink" href="#" target="_blank"></a></p>
        </div>
    </div>
    
    <script>
        const modalData = {
            thuvienphapluat: {
                title: 'Thư viện Pháp luật',
                description: 'Cơ sở dữ liệu văn bản pháp luật toàn diện nhất của Việt Nam, bao gồm Hiến pháp, Luật, Nghị định, Thông tư và các văn bản quy phạm pháp luật khác. Hỗ trợ tìm kiếm, tra cứu và so sánh văn bản.',
                link: 'https://thuvienphapluat.vn'
            },
            congbao: {
                title: 'Cổng Thông tin điện tử Chính phủ',
                description: 'Công bố chính thức các văn bản của Chính phủ, Thủ tướng Chính phủ và các Bộ, ngành. Bao gồm Nghị định, Quyết định, Chỉ thị và các văn bản chỉ đạo điều hành.',
                link: 'http://vanban.chinhphu.vn'
            },
            quochoi: {
                title: 'Cổng Thông tin điện tử Quốc hội',
                description: 'Văn bản pháp luật do Quốc hội, Ủy ban Thường vụ Quốc hội ban hành. Bao gồm Luật, Nghị quyết, Pháp lệnh và các văn bản khác của cơ quan lập pháp.',
                link: 'https://quochoi.vn'
            },
            gso: {
                title: 'Tổng cục Thống kê Việt Nam',
                description: 'Cơ quan thống kê chính thống của Việt Nam. Cung cấp số liệu về GDP, tăng trưởng kinh tế, lạm phát, xuất nhập khẩu, đầu tư, lao động, dân số và các chỉ tiêu kinh tế - xã hội khác.',
                link: 'https://www.gso.gov.vn'
            },
            sbv: {
                title: 'Ngân hàng Nhà nước Việt Nam',
                description: 'Ngân hàng trung ương Việt Nam. Cung cấp số liệu về chính sách tiền tệ, tỷ giá hối đoái, lãi suất, dự trữ ngoại hối, tín dụng ngân hàng, và các chỉ số tài chính vĩ mô.',
                link: 'https://www.sbv.gov.vn'
            },
            mof: {
                title: 'Bộ Tài chính',
                description: 'Thông tin về ngân sách nhà nước, chính sách thuế, nợ công, thị trường chứng khoán, dự toán và quyết toán ngân sách các cấp.',
                link: 'https://www.mof.gov.vn'
            },
            moit: {
                title: 'Bộ Công Thương',
                description: 'Số liệu về hoạt động xuất nhập khẩu, thương mại trong nước và quốc tế, sản xuất công nghiệp, năng lượng và các ngành công nghiệp.',
                link: 'https://www.moit.gov.vn'
            },
            worldbank: {
                title: 'World Bank Open Data',
                description: 'Cơ sở dữ liệu mở của Ngân hàng Thế giới về phát triển toàn cầu. Bao gồm chỉ số về GDP, đầu tư, nghèo đói, giáo dục, y tế, môi trường cho hơn 200 quốc gia.',
                link: 'https://data.worldbank.org'
            },
            imf: {
                title: 'International Monetary Fund Data',
                description: 'Dữ liệu của Quỹ Tiền tệ Quốc tế về tài chính quốc tế, cán cân thanh toán, tỷ giá, nợ nước ngoài, dự trữ ngoại hối và triển vọng kinh tế thế giới.',
                link: 'https://www.imf.org/en/Data'
            },
            adb: {
                title: 'Asian Development Bank',
                description: 'Ngân hàng Phát triển châu Á. Cung cấp số liệu kinh tế, báo cáo triển vọng phát triển và dự báo kinh tế cho các nước châu Á - Thái Bình Dương.',
                link: 'https://www.adb.org/data'
            },
            wto: {
                title: 'World Trade Organization Statistics',
                description: 'Tổ chức Thương mại Thế giới. Thống kê về thương mại quốc tế, rào cản thuế quan, cam kết thương mại đa phương và song phương.',
                link: 'https://www.wto.org/english/res_e/statis_e/statis_e.htm'
            },
            unctad: {
                title: 'UNCTAD Statistics',
                description: 'Hội nghị Liên Hợp Quốc về Thương mại và Phát triển. Dữ liệu về đầu tư trực tiếp nước ngoài (FDI), thương mại quốc tế và phát triển bền vững.',
                link: 'https://unctad.org/statistics'
            },
            googlescholar: {
                title: 'Google Scholar',
                description: 'Công cụ tìm kiếm miễn phí cho tài liệu học thuật, bài báo khoa học, luận văn, sách và bản tóm tắt từ nhiều nguồn học thuật.',
                link: 'https://scholar.google.com'
            },
            researchgate: {
                title: 'ResearchGate',
                description: 'Mạng xã hội học thuật cho nhà khoa học và nghiên cứu viên. Nơi chia sẻ bài báo, đặt câu hỏi và kết nối với cộng đồng nghiên cứu toàn cầu.',
                link: 'https://www.researchgate.net'
            },
            ssrn: {
                title: 'Social Science Research Network',
                description: 'Mạng nghiên cứu khoa học xã hội toàn cầu, chuyên về kinh tế, tài chính, kế toán, quản trị và luật. Cung cấp hàng triệu bài nghiên cứu và working papers.',
                link: 'https://www.ssrn.com'
            },
            jstor: {
                title: 'JSTOR Digital Library',
                description: 'Thư viện số chứa hàng triệu bài báo học thuật, sách và nguồn tài liệu chính từ nhiều lĩnh vực. Yêu cầu đăng ký hoặc truy cập qua thư viện đại học.',
                link: 'https://www.jstor.org'
            },
            nber: {
                title: 'National Bureau of Economic Research',
                description: 'Tổ chức nghiên cứu kinh tế tư nhân hàng đầu của Mỹ. Xuất bản working papers về kinh tế vĩ mô, tài chính, lao động và nhiều lĩnh vực khác.',
                link: 'https://www.nber.org'
            },
            vepr: {
                title: 'VEPR - Viện Nghiên cứu Kinh tế và Chính sách',
                description: 'Thuộc Đại học Quốc gia Hà Nội. Công bố báo cáo vĩ mô định kỳ, dự báo kinh tế Việt Nam, phân tích chính sách và tư vấn chính sách kinh tế.',
                link: 'http://vepr.org.vn'
            },
            ciem: {
                title: 'CIEM - Viện Nghiên cứu Quản lý Kinh tế Trung ương',
                description: 'Viện nghiên cứu trực thuộc Bộ Kế hoạch và Đầu tư. Nghiên cứu chính sách kinh tế vĩ mô, tích hợp kinh tế quốc tế, phát triển bền vững.',
                link: 'http://ciem.org.vn'
            },
            vcci: {
                title: 'VCCI - Phòng Thương mại và Công nghiệp Việt Nam',
                description: 'Tổ chức đại diện cho cộng đồng doanh nghiệp. Công bố Chỉ số Năng lực Cạnh tranh cấp tỉnh (PCI), báo cáo môi trường kinh doanh, chính sách hỗ trợ doanh nghiệp.',
                link: 'https://www.vcci.com.vn'
            },
            wef: {
                title: 'World Economic Forum',
                description: 'Diễn đàn Kinh tế Thế giới. Công bố Báo cáo Cạnh tranh Toàn cầu, Báo cáo Rủi ro Toàn cầu và các phân tích về xu hướng kinh tế - xã hội thế giới.',
                link: 'https://www.weforum.org/reports'
            },
            vneconomy: {
                title: 'VnEconomy',
                description: 'Báo điện tử chuyên sâu về kinh tế Việt Nam. Đưa tin về chính sách kinh tế, thị trường tài chính, doanh nghiệp và phân tích xu hướng kinh tế.',
                link: 'https://vneconomy.vn'
            },
            cafef: {
                title: 'CafeF',
                description: 'Trang tin tức tài chính hàng đầu Việt Nam. Chuyên về chứng khoán, bất động sản, ngân hàng, tài chính doanh nghiệp và thông tin doanh nghiệp niêm yết.',
                link: 'https://cafef.vn'
            },
            vietstock: {
                title: 'VietStock',
                description: 'Nền tảng thông tin và dữ liệu chứng khoán Việt Nam. Cung cấp báo cáo tài chính doanh nghiệp, phân tích kỹ thuật, tin tức thị trường và công cụ đầu tư.',
                link: 'https://vietstock.vn'
            }
        };
        
        function showModal(id, title, description, link) {
            const modal = document.getElementById('infoModal');
            const data = modalData[id] || { title: title, description: description, link: link };
            
            document.getElementById('modalTitle').textContent = data.title;
            document.getElementById('modalDescription').textContent = data.description;
            const linkElement = document.getElementById('modalLink');
            linkElement.href = data.link;
            linkElement.textContent = data.link;
            
            modal.style.display = 'block';
        }
        
        function closeModal() {
            document.getElementById('infoModal').style.display = 'none';
        }
        
        window.onclick = function(event) {
            const modal = document.getElementById('infoModal');
            if (event.target == modal) {
                modal.style.display = 'none';
            }
        }
        
        // Search functionality
        const searchInput = document.getElementById('searchInput');
        searchInput.addEventListener('input', function(e) {
            const searchTerm = e.target.value.toLowerCase();
            const nodes = document.querySelectorAll('.node');
            
            nodes.forEach(node => {
                node.classList.remove('highlight');
                const text = node.textContent.toLowerCase();
                if (searchTerm && text.includes(searchTerm)) {
                    node.classList.add('highlight');
                    // Scroll to first match
                    if (node.classList.contains('highlight')) {
                        setTimeout(() => {
                            node.scrollIntoView({ behavior: 'smooth', block: 'center' });
                        }, 100);
                    }
                }
            });
        });
    </script>
</body>
</html>
