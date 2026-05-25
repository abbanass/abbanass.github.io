<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Eid al-Adha Card Generator | Nass Media & Comm Tech</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
        body { font-family: 'Montserrat', sans-serif; }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen flex flex-col justify-between">

    <header class="bg-slate-900 border-b border-slate-800 py-4 px-6 sticky top-0 z-50 shadow-md">
        <div class="max-w-6xl mx-auto flex justify-between items-center">
            <h1 class="text-xl font-bold tracking-wide text-amber-400">NASS MEDIA & COMMUNICATIONS TECHNOLOGIES</h1>
            <span class="bg-emerald-500/10 text-emerald-400 text-xs px-2.5 py-1 rounded-full border border-emerald-500/20 flex items-center gap-1.5 font-mono">
                <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span> HTTPS SECURE
            </span>
        </div>
    </header>

    <main class="max-w-6xl w-full mx-auto p-4 md:p-8 grid grid-cols-1 lg:grid-cols-2 gap-8 items-start flex-grow">
        
        <div class="bg-slate-800/50 p-6 rounded-2xl border border-slate-700/60 shadow-xl backdrop-blur-sm">
            <h2 class="text-2xl font-bold text-white mb-2">Eid Greeting Generator</h2>
            <p class="text-slate-400 text-sm mb-6">Fill in your information below to personalize your official Eid Al-Adha 2026 greeting card.</p>
            
            <form id="cardForm" class="space-y-5">
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-2">Full Name</label>
                    <input type="text" id="fullName" placeholder="e.g., AHMED ABRAHAM" class="w-full bg-slate-900/80 border border-slate-700 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-amber-500 transition-colors">
                </div>

                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-2">Position / Rank</label>
                    <input type="text" id="position" placeholder="e.g., SENIOR MEDIA OFFICER" class="w-full bg-slate-900/80 border border-slate-700 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-amber-500 transition-colors">
                </div>

                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-2">Institution / Dept / Agency</label>
                    <input type="text" id="institution" placeholder="e.g., MINISTRY OF INFORMATION | KANO" class="w-full bg-slate-900/80 border border-slate-700 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-amber-500 transition-colors">
                </div>

                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-2">Upload Passport / Portrait Photo</label>
                    <label class="flex flex-col items-center justify-center border-2 border-dashed border-slate-700 hover:border-amber-500/50 rounded-xl py-6 cursor-pointer bg-slate-900/40 hover:bg-slate-900/80 transition-all group">
                        <svg class="w-8 h-8 text-slate-500 group-hover:text-amber-400 mb-2 transition-colors" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 002-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"></path></svg>
                        <span class="text-sm text-slate-300 font-medium group-hover:text-white">Choose Portrait Photo</span>
                        <span class="text-xs text-slate-500 mt-1">PNG or JPG preferred</span>
                        <input type="file" id="photoUpload" accept="image/*" class="hidden">
                    </label>
                </div>

                <button type="button" id="downloadBtn" class="w-full bg-gradient-to-r from-amber-500 to-amber-600 hover:from-amber-600 hover:to-amber-700 text-slate-950 font-bold py-3.5 px-6 rounded-xl transition-all shadow-lg shadow-amber-500/10 flex items-center justify-center gap-2 mt-8">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path></svg>
                    Download Custom Eid Card
                </button>
            </form>
        </div>

        <div class="flex flex-col items-center sticky top-24">
            <div class="text-xs font-semibold uppercase tracking-wider text-slate-400 mb-3 flex items-center gap-2 self-start pl-2">
                <span class="w-2 h-2 rounded-full bg-amber-400 animate-ping"></span> Live Generation Preview
            </div>
            
            <div class="relative bg-slate-950 rounded-2xl p-2 border border-slate-800 shadow-2xl max-w-sm w-full overflow-hidden">
                <canvas id="cardCanvas" class="w-full h-auto rounded-xl max-w-full block"></canvas>
            </div>
        </div>

    </main>

    <footer class="bg-slate-950 border-t border-slate-900 py-4 text-center text-xs text-slate-500">
        &copy; 2026 Nass Media and Communications Technologies. Empowering with Knowledge. Enriching with Technology.
    </footer>

    <script>
        const canvas = document.getElementById('cardCanvas');
        const ctx = canvas.getContext('2d');

        // Form Fields
        const fullNameInput = document.getElementById('fullName');
        const positionInput = document.getElementById('position');
        const institutionInput = document.getElementById('institution');
        const photoUpload = document.getElementById('photoUpload');
        const downloadBtn = document.getElementById('downloadBtn');

        // Design Specific Constants Extracted from Template
        const CANVAS_WIDTH = 800;
        const CANVAS_HEIGHT = 1200;
        
        // Exact Green Portrait Frame bounding box mappings
        const FRAME_X = 188;
        const FRAME_Y = 305;
        const FRAME_WIDTH = 424;
        const FRAME_HEIGHT = 538;

        let userImage = null;
        const templateImage = new Image();
        
        // Base64 encoded high-resolution asset background structure layout
        // For local development, replace this with your file path: templateImage.src = '1000662363.png';
        templateImage.src = 'https://i.ibb.co/67N5g86/1000662363.png'; 
        templateImage.crossOrigin = "anonymous"; // Bypass potential CORS security locks

        templateImage.onload = () => {
            canvas.width = CANVAS_WIDTH;
            canvas.height = CANVAS_HEIGHT;
            renderCanvas();
        };

        // Redraw canvas context pipeline cleanly
        function renderCanvas() {
            ctx.clearRect(0, 0, CANVAS_WIDTH, CANVAS_HEIGHT);
            
            // 1. Render User Portrait Photo inside the frame first if provided
            if (userImage) {
                ctx.save();
                // Clip output to exact boundaries of the template's picture window box area
                ctx.beginPath();
                ctx.rect(FRAME_X, FRAME_Y, FRAME_WIDTH, FRAME_HEIGHT);
                ctx.clip();

                // Object-fit: cover logic mathematically
                const imgRatio = userImage.width / userImage.height;
                const frameRatio = FRAME_WIDTH / FRAME_HEIGHT;
                let drawWidth, drawHeight, drawX, drawY;

                if (imgRatio > frameRatio) {
                    drawHeight = FRAME_HEIGHT;
                    drawWidth = userImage.width * (FRAME_HEIGHT / userImage.height);
                    drawX = FRAME_X + (FRAME_WIDTH - drawWidth) / 2;
                    drawY = FRAME_Y;
                } else {
                    drawWidth = FRAME_WIDTH;
                    drawHeight = userImage.height * (FRAME_WIDTH / userImage.width);
                    drawX = FRAME_X;
                    drawY = FRAME_Y + (FRAME_HEIGHT - drawHeight) / 2;
                }

                ctx.drawImage(userImage, drawX, drawY, drawWidth, drawHeight);
                ctx.restore();
            } else {
                // If empty, preserve the default stylized green chroma background matching image mockup
                ctx.fillStyle = "#4caf50";
                ctx.fillRect(FRAME_X, FRAME_Y, FRAME_WIDTH, FRAME_HEIGHT);
                
                // Add temporary indicator helper text contextually
                ctx.fillStyle = "#ffffff";
                ctx.font = "bold 24px Montserrat";
                ctx.textAlign = "center";
                ctx.fillText("[ Portrait Box Area ]", FRAME_X + (FRAME_WIDTH / 2), FRAME_Y + (FRAME_HEIGHT / 2));
            }

            // 2. Render core template framework over top layer safely
            ctx.drawImage(templateImage, 0, 0, CANVAS_WIDTH, CANVAS_HEIGHT);

            // 3. Render Personalized Text Inputs cleanly 
            ctx.textAlign = "center";
            
            // Full Name Line
            ctx.fillStyle = "#1e3d2f"; // Dark forest green matching branding
            ctx.font = "bold 34px Montserrat";
            const nameText = fullNameInput.value.trim().toUpperCase() || "FIRSTNAME LASTNAME";
            ctx.fillText(nameText, 400, 915);

            // Position Line
            ctx.fillStyle = "#1e3d2f";
            ctx.font = "600 24px Montserrat";
            const posText = positionInput.value.trim().toUpperCase() || "POSITION / RANK";
            ctx.fillText(posText, 400, 955);

            // Institution Details Line
            ctx.fillStyle = "#556b60"; // Lighter contrast tone
            ctx.font = "500 19px Montserrat";
            const instText = institutionInput.value.trim().toUpperCase() || "INSTITUTION | DEPT | AGENCY";
            ctx.fillText(instText, 400, 992);

            // Embedded Date calculations automatically dynamically loaded
            ctx.fillStyle = "#f59e0b"; // Premium Gold tone context
            ctx.font = "bold 20px Montserrat";
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            const todayText = new Date().toLocaleDateString('en-US', options);
            ctx.fillText(todayText, 400, 1032);
        }

        // Live Event Listeners reflecting instant modifications 
        fullNameInput.addEventListener('input', renderCanvas);
        positionInput.addEventListener('input', renderCanvas);
        institutionInput.addEventListener('input', renderCanvas);

        // Portrait Image file intake management flow
        photoUpload.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (event) => {
                    const img = new Image();
                    img.onload = () => {
                        userImage = img;
                        renderCanvas();
                    };
                    img.src = event.target.result;
                };
                reader.readAsDataURL(file);
            }
        });

        // Trigger secure base64 download directly down to file directory on user machine
        downloadBtn.addEventListener('click', () => {
            const link = document.createElement('a');
            link.download = `Eid_AlAdha_Card_2026_${fullNameInput.value.replace(/\s+/g, '_') || 'NassMedia'}.png`;
            link.href = canvas.toDataURL('image/png');
            link.click();
        });
    </script>
</body>
</html>
