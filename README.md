<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generate QR Code</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <style>
       body {
            font-family: Arial, sans-serif;
            background-color: #f2f2f2;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            height: 100vh;
        }

        .box {
            text-align: center;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            max-width: 800px;
            width: 100%;
            margin-top: 20px; /* Ensure there's space above the box */
        }

        .input-group {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .input-group input, .input-group select, .input-group button {
            padding: 10px;
            margin: 10px;
            border-radius: 5px;
            border: 1px solid #ddd;
            font-size: 16px;
            width: 100%;
            max-width: 300px;
        }

        .input-group button {
            background-color: #333;
            color: white;
            cursor: pointer;
        }

        .input-group button:hover {
            background-color: #555;
        }

        .qr-code {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin: 10px;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 300px;
        }

        .qr-code p {
            margin: 10px 0 0;
            font-size: 14px;
            color: #333;
        }

        #qr-codes-container {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            justify-content: center;
            width: 100%;
            max-width: 800px;
            margin-bottom: 20px; /* Ensure there's space below the QR codes */
        }

        /* Responsive Styles */
        @media (max-width: 600px) {
            .input-group input, .input-group select, .input-group button {
                max-width: 100%;
            }

            .qr-code {
                width: 100%;
            }

            body {
                padding: 10px;
                height: auto;
            }

            .box {
                width: 100%;
                padding: 15px;
            }
        }
    </style>
</head>
<body>
    <div id="qr-codes-container"></div> <!-- QR Codes Container at the Top -->
    
    <div class="box">
        <div class="input-group">
            <input id="qr-text" type="text" placeholder="QR code text">
            <select id="sizes">
                <optgroup label="GS">
                    <option value="P10311001010800BC39000800F240206-6001000250">bleed screw</option>
                    <option value="P10311001010804BC58610400F240206-600100020">CKD seal piston</option>
                    <option value="P10311001010800BC38002400F240206-6001000250">LOCAL SEAL PISTON</option>
                    <option value="P10311001010800BC45000700F240206-6001000240">BOOT PISTON</option>
                    <option value="P10311001010800BC30202100F240206-6001000290">PISTON</option>
                    <option value="P10311001010800BC43101300F240206-6001000270">54 GUIDE ROD A</option>
                    <option value="P10311001010800BC44101300F240206-6001000260">54 GUIDE ROD B</option>
                    <option value="P10318427010400BC45000700A1069425-B,C000240">BOOT GUIDE</option>
                    <option value="P10311001010800BC470B0500F240206-6001000210">SP2I SPRING PAD</option>
                    <option value="P10311001010800BC47028900F240206-6001000210">QXI SPRING PAD</option>
                    <option value="P10311001010800BC39100500F240206-6001000230">BLEED SCREW CAP</option>
                    <option value="P10311001010800BC46000400F240206-6001000200">BOLT</option>
                    <option value="P10311001010800BM38002100F240206-6001000260">PROTECTIVE PLUG</option>
                    <option value="P10311001010800BC44200700F240206-6001000250">54 bush</option>
                </optgroup>
                <optgroup label="51">
                    <option value="P10311001010800BC38002800F240206-6001000240">Option 51-seal piston</option>
                    <option value="P10311001010800BC36000800F240206-6001000250">Option 51-BA Boot piston</option>
                    <option value="P10311001010800BC47028400F240206-6001000290">Option 51-AH2 SPRING PAD</option>
                    <option value="P10311001010800BC38002800F240206-6001000230">Option 52-BA SPRING PAD</option>
                    <option value="P10311001010800BC38002800F240206-6001000200">Option 51-BUSH</option>
                    <option value="P10311001010800BC56003900F240206-6001000280">BA RETURN SPRING</option>
                    <option value="P10311001010800BC43101400F240206-6001000240">A</option>
                    <option value="P10311001010800BC44101500F240206-6001000260">B</option>
                    <option value="P10311001010800BC30207600F240206-6001000270">BA piston</option>
                    <option value="P10311001010800BC45000800F240206-6001000290">BA boot guide rod</option>
                    <option value="P10311001010800BC44200800F240206-6001000220">BA Bush</option>
                    <option value="P10318427011400BC45000700A1069425-B,C000200">BA Bush</option>
                </optgroup>
                <optgroup label="54">
                    <option value="D202408060504 BC410A7200">qxi rh</option>
                    <option value="D202408060504 BC121A7101">qxi carrier</option>
                </optgroup>
            </select>
            <button onclick="generateSingleQRCode()">Generate Single QR Code</button>
            <button onclick="generateAllQRCodes()">Generate All QR Codes</button>
        </div>
    </div>

    <script>
        function generateRandomizedSize(size) {
            // Replace the 11th and 12th characters with random digits
            let randomDigit1 = Math.floor(Math.random() * 10);
            let randomDigit2 = Math.floor(Math.random() * 10);
            return size.slice(0, 10) + randomDigit1 + randomDigit2 + size.slice(12);
        }

        function generateQRCode(text, size) {
            const qrContent = text + " " + size;
            const qrCodeDiv = document.createElement("div");
            qrCodeDiv.className = "qr-code";
            new QRCode(qrCodeDiv, {
                text: qrContent,
                width: 200,
                height: 200,
            });
            const label = document.createElement("p");
            label.textContent = qrContent;
            qrCodeDiv.appendChild(label);
            return qrCodeDiv;
        }

        function generateSingleQRCode() {
            const text = document.getElementById("qr-text").value;
            let size = document.getElementById("sizes").value;
            const container = document.getElementById("qr-codes-container");

            container.innerHTML = ''; // Clear existing QR codes

            size = generateRandomizedSize(size);
            const qrCode = generateQRCode(text, size);
            container.appendChild(qrCode);
        }

        function generateAllQRCodes() {
            const text = document.getElementById("qr-text").value;
            const options = document.querySelectorAll("#sizes option");
            const container = document.getElementById("qr-codes-container");

            container.innerHTML = ''; // Clear existing QR codes

            options.forEach(option => {
                let size = option.value;
                size = generateRandomizedSize(size);
                const qrCode = generateQRCode(text, size);
                container.appendChild(qrCode);
            });
        }
    </script>
</body
