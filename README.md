<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OTP</title>
    <script>
        async function generateOTP() {
            const service = document.getElementById("service").value;
            const response = await fetch("/generate", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ service }),
            });
            const data = await response.json();
            if (data.otp) {
                document.getElementById("otp").innerText = `OTP: ${data.otp} (expira en ${data.expires_in} segundos)`;
            } else {
                alert(data.error);
            }
        }

        async function validateOTP() {
            const service = document.getElementById("service").value;
            const otp = document.getElementById("otpInput").value;
            const response = await fetch("/validate", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ service, otp }),
            });
            const data = await response.json();
            alert(data.success || data.error);
        }
    </script>
</head>
<body>
    <h1>Generator & Validator</h1>
    <label for="service">Servicio:</label>
    <select id="service">
        <option value="amazon">Amazon</option>
        <option value="walmart">Walmart</option>
    </select>
    <br><br>
    <button onclick="generateOTP()">Generar OTP</button>
    <p id="otp"></p>
    <hr>
    <h2>Validar OTP</h2>
    <input type="text" id="otpInput" placeholder="Introduce el OTP">
    <button onclick="validateOTP()">Validar</button>
</body>
</html>
Musiando/Musiando is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
