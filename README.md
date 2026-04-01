<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>정관 자동 생성기 (상법 기준)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@400;700&display=swap');
        .preview-font { font-family: 'Noto Serif KR', serif; }
        /* 스크롤바 스타일링 */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
    </style>
</head>
<body class="bg-gray-100 min-h-screen flex flex-col md:flex-row font-sans">

    <!-- 좌측: 입력 패널 -->
    <div class="w-full md:w-2/5 p-6 bg-white shadow-lg border-r overflow-y-auto h-screen">
        <div class="flex items-center gap-3 mb-6 pb-4 border-b border-gray-200">
            <div class="p-2 bg-blue-600 rounded-md">
                <i data-lucide="book-open" class="text-white w-5 h-5"></i>
            </div>
            <h1 class="text-xl font-bold text-gray-800">정관 자동 생성기 (상법 기준)</h1>
        </div>

        <div class="space-y-8">
            <!-- 제1장 총칙 항목 -->
            <section>
                <div class="flex items-center gap-2 mb-3 text-blue-700 font-bold">
                    <i data-lucide="building-2" class="w-4 h-4"></i>
                    <h2>제1장 총칙 (상법 제289조)</h2>
                </div>
                <div class="bg-gray-50 p-4 rounded-lg space-y-4 border border-gray-200">
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-1">상호</label>
                        <input type="text" id="companyName" value="주식회사 더블유오엔" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 outline-none text-sm" oninput="updatePreview()">
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-1">본점 소재지</label>
                            <input type="text" id="location" value="서울특별시" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 text-sm" oninput="updatePreview()">
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-1">공고 방법</label>
                            <input type="text" id="announcementMedia" value="선경일보" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 text-sm" oninput="updatePreview()">
                        </div>
                    </div>
                    <div>
                        <div class="flex items-center justify-between mb-2">
                            <label class="block text-sm font-semibold text-gray-700">목적 (사업 내용)</label>
                            <button onclick="addPurpose()" class="text-xs bg-white border border-blue-200 hover:bg-blue-50 text-blue-600 px-2 py-1 rounded flex items-center gap-1 shadow-sm">
                                <i data-lucide="plus" class="w-3 h-3"></i> 추가
                            </button>
                        </div>
                        <div id="purposesContainer" class="space-y-2 max-h-60 overflow-y-auto pr-2">
                            <!-- 목적 리스트 렌더링 영역 -->
                        </div>
                    </div>
                </div>
            </section>

            <!-- 제2장 주식 항목 -->
            <section>
                <div class="flex items-center gap-2 mb-3 text-blue-700 font-bold">
                    <i data-lucide="circle-dollar-sign" class="w-4 h-4"></i>
                    <h2>제2장 주식 및 자본</h2>
                </div>
                <div class="bg-gray-50 p-4 rounded-lg grid grid-cols-2 gap-4 border border-gray-200">
                    <div class="col-span-2">
                        <label class="block text-sm font-semibold text-gray-700 mb-1">발행할 주식의 총수</label>
                        <input type="text" id="totalShares" value="1,000,000" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 text-sm" oninput="updatePreview()">
                    </div>
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-1">1주의 금액 (액면가)</label>
                        <input type="text" id="sharePrice" value="1,000" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 text-sm" oninput="updatePreview()">
                    </div>
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-1">설립 시 발행주식총수</label>
                        <input type="text" id="initialShares" value="20,000" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 text-sm" oninput="updatePreview()">
                    </div>
                </div>
            </section>

            <!-- 제5장 임원 및 부칙 항목 -->
            <section>
                <div class="flex items-center justify-between mb-3 text-blue-700 font-bold">
                    <div class="flex items-center gap-2">
                        <i data-lucide="users" class="w-4 h-4"></i>
                        <h2>임원 및 발기인 (제5장/부칙)</h2>
                    </div>
                    <button onclick="addFounder()" class="text-xs bg-white border border-blue-200 hover:bg-blue-50 text-blue-600 px-2 py-1 rounded flex items-center gap-1 shadow-sm">
                        <i data-lucide="plus" class="w-3 h-3"></i> 발기인 추가
                    </button>
                </div>
                <div class="bg-gray-50 p-4 rounded-lg space-y-4 border border-gray-200">
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-1">이사 수</label>
                            <input type="number" id="directorsCount" value="1" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 text-sm" oninput="updatePreview()">
                        </div>
                        <div class="flex items-center pt-5">
                            <label class="flex items-center gap-2 cursor-pointer">
                                <input type="checkbox" id="hasAuditor" class="w-4 h-4 text-blue-600 rounded border-gray-300" onchange="updatePreview()">
                                <span class="text-sm font-semibold text-gray-700">감사 선임 필수</span>
                            </label>
                        </div>
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-1">영업년도 시작월</label>
                            <input type="text" id="fiscalYearStart" value="1" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 text-sm" oninput="updatePreview()">
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-1">영업년도 종료월</label>
                            <input type="text" id="fiscalYearEnd" value="12" class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 text-sm" oninput="updatePreview()">
                        </div>
                    </div>
                    
                    <div class="space-y-3">
                        <label class="block text-sm font-semibold text-gray-700">발기인 명세</label>
                        <div id="foundersContainer" class="space-y-3">
                            <!-- 발기인 리스트 렌더링 영역 -->
                        </div>
                    </div>
                </div>
            </section>
        </div>
    </div>

    <!-- 우측: 실시간 문서 프리뷰 -->
    <div class="w-full md:w-3/5 p-6 flex flex-col h-screen">
        <div class="flex justify-between items-center mb-4 bg-white p-3 rounded-lg border shadow-sm">
            <h2 class="text-sm font-bold text-gray-700 flex items-center gap-2">
                <i data-lucide="file-text" class="text-blue-600 w-4 h-4"></i>
                정관 출력 미리보기
            </h2>
            <button onclick="copyToClipboard()" id="copyBtn" class="flex items-center gap-1.5 bg-gray-800 text-white hover:bg-gray-700 px-3 py-1.5 rounded text-sm font-bold transition-colors">
                <i data-lucide="copy" class="w-4 h-4" id="copyIcon"></i>
                <span id="copyText">문서 전체 복사</span>
            </button>
        </div>
        
        <div id="previewContent" class="flex-1 bg-white border border-gray-300 shadow-sm rounded-lg p-10 overflow-y-auto preview-font text-[15px] leading-7 text-gray-900 whitespace-pre-wrap">
            <!-- 프리뷰 내용 렌더링 영역 -->
        </div>
    </div>

    <script>
        // 초기 데이터 세팅
        let purposes = [
            '사진촬영 및 처리업', '앨범사진 촬영업', '인물사진 및 행사용 영상 촬영업',
            '시각 디자인업, 그래픽 디자인업', '광고 디자인업, 디자인 용역', '인테리어 디자인업',
            '공연 기획 및 연출, 제작업', '컴퓨터 프로그래밍 시스템 개발, 관리, 유지, 보수업',
            '홈페이지 개발, 제작, 공급업', '인터넷 쇼핑몰 운영, 개발, 제작업',
            '의류 및 의류 잡화 도.소매업', '온라인 광고업 및 온라인 광고대행업',
            '사진, 영상 촬영용 기자재 임대업', '경영 컨설팅업', '인쇄업',
            '전자상거래 소매업', '공간 대여업', '공간 대여 렌탈업',
            '서비스업', '부동산 임대업', '각호에 관련된 전자상거래업 및 통신판매업'
        ];

        let founders = [
            { name: '김지원', registrationNumber: '920224-XXXXXXX', address: '경기도 광주시 태성1로 16, 103동 2405호' }
        ];

        const creationDate = new Date().toLocaleDateString('ko-KR', { year: 'numeric', month: 'long', day: 'numeric' });

        // 아이콘 초기화
        lucide.createIcons();

        // 목적 렌더링
        function renderPurposes() {
            const container = document.getElementById('purposesContainer');
            container.innerHTML = '';
            purposes.forEach((purpose, index) => {
                const div = document.createElement('div');
                div.className = 'flex gap-2 items-center';
                div.innerHTML = `
                    <span class="text-gray-400 text-xs w-4">${index + 1}.</span>
                    <input type="text" value="${purpose}" oninput="updatePurpose(${index}, this.value)" class="flex-1 p-1.5 border border-gray-300 rounded text-sm focus:ring-2 focus:ring-blue-500 outline-none">
                    <button onclick="removePurpose(${index})" class="text-gray-400 hover:text-red-500 transition-colors">
                        <i data-lucide="trash-2" class="w-4 h-4"></i>
                    </button>
                `;
                container.appendChild(div);
            });
            lucide.createIcons();
            updatePreview();
        }

        // 목적 조작 함수들
        function updatePurpose(index, value) { purposes[index] = value; updatePreview(); }
        function addPurpose() { purposes.push(''); renderPurposes(); }
        function removePurpose(index) { purposes.splice(index, 1); renderPurposes(); }

        // 발기인 렌더링
        function renderFounders() {
            const container = document.getElementById('foundersContainer');
            container.innerHTML = '';
            founders.forEach((founder, index) => {
                const div = document.createElement('div');
                div.className = 'p-3 bg-white border border-gray-200 rounded relative group shadow-sm';
                div.innerHTML = `
                    <button onclick="removeFounder(${index})" class="absolute top-2 right-2 text-gray-300 hover:text-red-500 transition-colors">
                        <i data-lucide="trash-2" class="w-4 h-4"></i>
                    </button>
                    <div class="grid gap-2">
                        <div class="grid grid-cols-2 gap-2">
                            <input type="text" placeholder="성명" value="${founder.name}" oninput="updateFounder(${index}, 'name', this.value)" class="p-1.5 text-sm border border-gray-300 rounded bg-gray-50 focus:bg-white focus:ring-2 focus:ring-blue-500 outline-none">
                            <input type="text" placeholder="주민등록번호" value="${founder.registrationNumber}" oninput="updateFounder(${index}, 'registrationNumber', this.value)" class="p-1.5 text-sm border border-gray-300 rounded bg-gray-50 focus:bg-white focus:ring-2 focus:ring-blue-500 outline-none">
                        </div>
                        <input type="text" placeholder="주소" value="${founder.address}" oninput="updateFounder(${index}, 'address', this.value)" class="p-1.5 text-sm border border-gray-300 rounded w-full bg-gray-50 focus:bg-white focus:ring-2 focus:ring-blue-500 outline-none">
                    </div>
                `;
                container.appendChild(div);
            });
            lucide.createIcons();
            updatePreview();
        }

        // 발기인 조작 함수들
        function updateFounder(index, field, value) { founders[index][field] = value; updatePreview(); }
        function addFounder() { founders.push({ name: '', registrationNumber: '', address: '' }); renderFounders(); }
        function removeFounder(index) { founders.splice(index, 1); renderFounders(); }

        // 미리보기 업데이트 메인 함수
        function updatePreview() {
            const companyName = document.getElementById('companyName').value;
            const location = document.getElementById('location').value;
            const announcementMedia = document.getElementById('announcementMedia').value;
            const totalShares = document.getElementById('totalShares').value;
            const sharePrice = document.getElementById('sharePrice').value;
            const initialShares = document.getElementById('initialShares').value;
            const directorsCount = document.getElementById('directorsCount').value;
            const hasAuditor = document.getElementById('hasAuditor').checked;
            const fiscalYearStart = document.getElementById('fiscalYearStart').value;
            const fiscalYearEnd = document.getElementById('fiscalYearEnd').value;

            const purposesText = purposes.map((p, i) => `    ${i + 1}. ${p}`).join('\n');
            const foundersText = founders.map(f => `발기인: ${f.name} (${f.registrationNumber})\n주소: ${f.address}`).join('\n\n');

            const template = `정     관

${companyName}

제 1장  총      칙

제 1조 (상 호)
 본 회사는 ${companyName}(이)라 한다.

제 2조 (목 적) 
 본 회사는 다음 사업을 경영함을 목적으로 한다.
${purposesText}
    ${purposes.length + 1}. 각 호에 관련된 부대사업 일체

제 3조 (본점의 소재지 및 지점등의 설치) 
 ① 본 회사의 본점은 ${location}내에 둔다.
 ② 본 회사는 필요에 따라 이사회의 결의로 국내.외에 지점 및 영업소를 둘 수 있다.

제 4조 (공고 방법)
 본 회사의 공고는 ${location}내에서 발행되는 일간 ${announcementMedia}에 게재한다.

제 2장  주식과 주권

제 5조 (회사가 발행할 주식의 총수)
 본 회사가 발행할 주식의 총수는 ${totalShares} 주로 한다.

제 6조 (1주의 금액)
 본 회사가 발행하는 주식 1주의 금액은 금 ${sharePrice}원으로 한다.

제 7조 (회사의 설립시에 발행하는 주식 총수 및 그 종류)
 본 회사가 설립 시에 발행하는 주식의 총수는 보통주 ${initialShares}주로 한다.

제 8조 (주권의 종류)
 본 회사의 주식은 보통주식으로서 전부 기명식으로 하고 주권은 1주권, 10주권, 100주권, 500주권, 1,000주권의 5종으로 한다.

제 9조 (신주인수권)
 ① 본 회사의 주주는 신주발행에 있어서 그가 소유한 주식 수에 비례하여 신주의 배정을 받을 권리를 가진다.

제 3장 사 채
(중략)

제 4장 주 주 총 회
제 21조 (소집)
 ① 본 회사의 정기주주총회는 영업년도 말일의 다음날부터 3월 이내에 소집하고, 임시주주총회는 필요한 경우에 수시 소집한다.

제 5 장  임   원 
제 27조 (임원의 원수 및 선임)
  ① 본 회사의 이사는 ${directorsCount}인 이상으로 하고, ${hasAuditor ? '감사를 둔다' : '감사를 둘 수 있다'}. 단, 자본금이 10억 이상으로 되는 경우에는 이사는 3인 이상, 감사는 1인 이상으로 한다. 

제 6장  계         산
제 38조 (영업년도)
 본 회사의 영업년도는 매년 ${fiscalYearStart}월 1일부터 동년 ${fiscalYearEnd}월 31일까지로 한다.

제 39조 (재무제표 등의 작성비치)
  (중략)
  ② 제1항의 서류는 정기주주총회 1주간 전부터 당 회사의 본점과 지점에 비치하여야 하고, 총회의 승인을 얻었을 때에는 그 중 재무상태표를 지체없이 공고하여야 한다.

제 40조 (이익금의 처분)
  매기 총수입금에서 총지출금을 공제한 잔액을 이익금(전기이월금 포함)으로 하여 이를 다음과 같이 처분한다.
    1. 이익준비금(금전에 의한 이익배당액의 10분의 1이상)
    2. 기타의 법정적립금
    3. 별도적립금 
    4. 주주배당금   
    5. 임원상여금
    6. 임의적립금
    7. 차기이월금

제 41조 (이익 배당)
  ① 이익의 배당은 금전과 주식으로 할 수 있다.
  ② 전항의 배당은 매 결산기말 현재의 주주명부에 기재된 주주 또는 등록된 질권자에게 지급한다. 
  ③ 이익의 배당을 주식으로 하는 경우 회사가 수종의 주식을 발행한 때에는 주주총회의 결의로 그와 다른 종류의 주식으로 배당할 수 있다.

부            칙
제 1조 (최초의 영업년도)
 본 회사의 최초의 영업연도는 회사설립일로부터 동년 ${fiscalYearEnd}월 31일까지로 한다.

제 3조(발기인의 성명, 주소)
 본 회사 발기인의 성명, 주민등록번호, 주소는 다음과 같다.

${foundersText}

이상과 같이 정관을 작성하고 발기인이 서명 또는 기명날인 한다.

${creationDate}`;

            document.getElementById('previewContent').innerText = template;
        }

        // 클립보드 복사 함수 (호환성 확보)
        function copyToClipboard() {
            const textToCopy = document.getElementById('previewContent').innerText;
            const textArea = document.createElement("textarea");
            textArea.value = textToCopy;
            document.body.appendChild(textArea);
            textArea.select();
            
            try {
                document.execCommand('copy');
                
                // UI 피드백 변경
                const btn = document.getElementById('copyBtn');
                const text = document.getElementById('copyText');
                
                btn.className = "flex items-center gap-1.5 bg-green-100 text-green-700 border border-green-200 px-3 py-1.5 rounded text-sm font-bold transition-colors";
                text.innerText = "클립보드 복사 완료";
                btn.innerHTML = `<i data-lucide="check" class="w-4 h-4"></i> <span id="copyText">클립보드 복사 완료</span>`;
                lucide.createIcons();

                // 2초 후 원상복구
                setTimeout(() => {
                    btn.className = "flex items-center gap-1.5 bg-gray-800 text-white hover:bg-gray-700 px-3 py-1.5 rounded text-sm font-bold transition-colors";
                    btn.innerHTML = `<i data-lucide="copy" class="w-4 h-4"></i> <span id="copyText">문서 전체 복사</span>`;
                    lucide.createIcons();
                }, 2000);
            } catch (err) {
                alert('복사에 실패했습니다. 수동으로 복사해주세요.');
            }
            
            document.body.removeChild(textArea);
        }

        // 초기 실행
        renderPurposes();
        renderFounders();
    </script>
</body>
</html>
