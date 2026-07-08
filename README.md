# Yohan--info-2
Un site d'information 
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yohan Info - L'Actualité Vérifiée</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        /* Effet de flou pour les articles Premium non payés */
        .text-verrouille {
            filter: blur(5px);
            user-select: none;
            pointer-events: none;
        }
    </style>
</head>
<body class="bg-gray-900 text-gray-100 font-sans min-h-screen flex flex-col">

    <header class="bg-gray-800 border-b border-gray-700 sticky top-0 z-50 px-4 py-3 flex justify-between items-center">
        <h1 class="text-xl font-black text-amber-500 tracking-wider flex items-center gap-2 uppercase">
            <i data-lucide="globe" class="text-amber-500"></i> YOHAN INFO
        </h1>
        <button onclick="ouvrirPremium()" class="bg-gradient-to-r from-amber-500 to-orange-500 text-gray-900 font-black px-4 py-2 rounded-full text-xs flex items-center gap-1.5 shadow-lg active:scale-95">
            <i data-lucide="crown" class="w-4 h-4"></i> ACCÈS PREMIUM
        </button>
    </header>

    <div class="bg-gray-800 border-b border-gray-700 px-4 py-2 flex justify-between items-center text-xs">
        <span class="text-emerald-400 flex items-center gap-1 font-medium">
            <span class="w-2 h-2 bg-emerald-500 rounded-full animate-ping"></span>
            Mises à jour chaque heure
        </span>
        <span id="prochaine-maj" class="text-gray-400 font-mono">Synchro : 59m 59s</span>
    </div>

    <div id="notif-push" class="fixed bottom-4 left-4 right-4 bg-amber-500 text-gray-900 p-3 rounded-xl shadow-2xl z-50 transform translate-y-32 transition-transform duration-500 flex items-center gap-3">
        <div class="bg-gray-900 text-amber-500 p-2 rounded-lg"><i data-lucide="bell" class="w-5 h-5 animate-bounce"></i></div>
        <div class="flex-1">
            <h4 class="text-xs font-black uppercase">Exclusivité Yohan Info</h4>
            <p id="notif-texte" class="text-xs font-medium line-clamp-1"></p>
        </div>
        <button onclick="fermerNotif()" class="text-gray-900 p-1"><i data-lucide="x" class="w-4 h-4"></i></button>
    </div>

    <main class="flex-1 p-4 max-w-md mx-auto w-full space-y-4 pb-24">
        
        <div class="flex items-center justify-between">
            <h2 class="text-xs font-bold text-gray-400 uppercase tracking-wider flex items-center gap-1.5">
                <i data-lucide="rss" class="w-4 h-4 text-amber-500"></i> Fil d'actualités réelles
            </h2>
            <button onclick="chargerActualites(true)" class="text-xs text-amber-500 bg-gray-800 px-2.5 py-1 rounded-lg border border-gray-700">
                <i data-lucide="refresh-cw" class="w-3 h-3"></i> Actualiser
            </button>
        </div>

        <div id="loader" class="text-center py-16 space-y-3">
            <div class="w-8 h-8 border-4 border-amber-500 border-t-transparent rounded-full animate-spin mx-auto"></div>
            <p class="text-xs text-gray-400">Téléchargement des dépêches en direct...</p>
        </div>

        <div id="flux-actus" class="space-y-4 hidden"></div>

    </main>

    <div id="modal-premium" class="hidden fixed inset-0 bg-black/80 z-50 flex items-center justify-center p-4 backdrop-blur-md">
        <div class="bg-gray-800 border border-gray-700 rounded-3xl w-full max-w-sm p-6 relative shadow-2xl">
            <button onclick="fermerPremium()" class="absolute top-4 right-4 text-gray-400 hover:text-white bg-gray-900 p-1.5 rounded-full border border-gray-700">
                <i data-lucide="x" class="w-4 h-4"></i>
            </button>

            <div class="text-center space-y-4">
                <div class="w-14 h-14 bg-amber-500/10 text-amber-500 rounded-full flex items-center justify-center mx-auto border border-amber-500/20">
                    <i data-lucide="crown" class="w-7 h-7"></i>
                </div>
                
                <div>
                    <h3 class="text-xl font-black">Abonnement Yohan Info Privé</h3>
                    <p class="text-xs text-gray-400 mt-1">Débloquez toutes les analyses confidentielles, les coulisses politiques et supprimez le flou.</p>
                </div>
                
                <div class="bg-gray-900 p-3 rounded-2xl border border-gray-700 flex justify-between items-center px-4">
                    <span class="text-xs text-gray-400 font-medium">Tarif d'accès</span>
                    <span class="text-xl font-black text-amber-500">1 000 FCFA <span class="text-[10px] text-gray-400 font-normal">/ mois</span></span>
                </div>

                <div class="space-y-2.5 pt-2">
                    <a href="https://checkout.fedapay.com/votre-lien-carte-bancaire" target="_blank" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold py-3 px-4 rounded-xl flex items-center justify-between transition text-xs shadow-lg">
                        <span class="flex items-center gap-2"><i data-lucide="credit-card" class="w-4 h-4"></i> Carte (Visa / Mastercard)</span>
                        <i data-lucide="chevron-right" class="w-4 h-4"></i>
                    </a>

                    <a href="https://pay.wave.com/m/c-ci-0576721245?amount=1000" target="_blank" class="w-full bg-[#1CA3DE] hover:bg-[#1582B3] text-white font-bold py-3 px-4 rounded-xl flex items-center justify-between transition text-xs shadow-lg">
                        <span class="flex items-center gap-2"><i data-lucide="smartphone" class="w-4 h-4"></i> Application Wave</span>
                        <i data-lucide="chevron-right" class="w-4 h-4"></i>
                    </a>
                </div>
                
                <div class="pt-3 border-t border-gray-700/50 text-left bg-gray-900/50 p-3 rounded-xl border border-gray-700/30">
                    <p class="text-[10px] text-gray-400">💡 **Alternative Manuelle :** Si les boutons automatiques ne réagissent pas sur votre smartphone, faites un transfert Wave direct au :</p>
                    <p class="text-xs font-mono font-bold text-amber-500 text-center mt-2 p-1.5 bg-gray-900 rounded border border-gray-700 select-all">
                        +225 0576721245
                    </p>
                </div>
            </div>
        </div>
    </div>

    <script>
        const API_FLUX = "https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Fwww.france24.com%2Ffr%2Fafrique%2Frss";
        let tempsRestant = 3600;

        function demarrerChrono() {
            setInterval(() => {
                tempsRestant--;
                if (tempsRestant <= 0) { tempsRestant = 3600; chargerActualites(true); }
                const mins = Math.floor(tempsRestant / 60);
                const secs = tempsRestant % 60;
                document.getElementById('prochaine-maj').innerText = `Synchro : ${mins}m ${secs}s`;
            }, 1000);
        }

        async function chargerActualites(notifier = false) {
            const loader = document.getElementById('loader');
            const conteneur = document.getElementById('flux-actus');
            
            if(!notifier) { loader.classList.remove('hidden'); conteneur.classList.add('hidden'); }

            try {
                const rep = await fetch(API_FLUX);
                const data = await rep.json();

                if (data.status === 'ok') {
                    conteneur.innerHTML = '';
                    
                    data.items.forEach((article, index) => {
                        const estPremium = index % 2 === 0; 
                        
                        const card = document.createElement('div');
                        card.className = "bg-gray-800 border border-gray-700 rounded-2xl p-4 space-y-3 shadow-md relative overflow-hidden";
                        
                        let img = '';
                        if (article.enclosure?.link) {
                            img = `<img src="${article.enclosure.link}" class="w-full h-40 object-cover rounded-xl ${estPremium ? 'text-verrouille' : ''}">`;
                        }

                        const textePropre = article.description.replace(/<[^>]*>/g, '').substring(0, 140) + '...';

                        card.innerHTML = `
                            ${img}
                            <div class="flex justify-between items-center">
                                <span class="text-[9px] font-black uppercase px-2 py-0.5 rounded ${estPremium ? 'bg-amber-500 text-gray-900' : 'bg-gray-700 text-gray-300'} tracking-wider">
                                    ${estPremium ? '⭐ PREMIUM' : 'GRATUIT'}
                                </span>
                                <div class="text-[10px] text-emerald-400 bg-emerald-500/10 px-2 py-0.5 rounded-full font-bold flex items-center gap-1">
                                    <i data-lucide="shield-check" class="w-3 h-3"></i> CERTIFIÉ
                                </div>
                            </div>
                            
                            <h3 class="text-sm font-bold text-white">${article.title}</h3>
                            
                            <p class="text-xs text-gray-300 leading-relaxed ${estPremium ? 'text-verrouille' : ''}">
                                ${textePropre}
                            </p>

                            ${estPremium ? `
                            <div class="absolute inset-x-0 bottom-0 bg-gradient-to-t from-gray-800 via-gray-800/90 to-transparent pt-12 pb-4 px-4 flex flex-col items-center justify-center text-center">
                                <p class="text-xs font-bold text-amber-400 mb-2 flex items-center gap-1">
                                    <i data-lucide="lock" class="w-3.5 h-3.5"></i> Contenu exclusif Yohan Info
                                </p>
                                <button onclick="ouvrirPremium()" class="bg-amber-500 hover:bg-amber-600 text-gray-900 text-[11px] font-black px-4 py-1.5 rounded-xl transition">
                                    Débloquer pour 1 000 FCFA
                                </button>
                            </div>
                            ` : `
                            <div class="flex justify-between items-center pt-2 border-t border-gray-700/50 text-[10px] text-gray-400">
                                <span>Source d'Information</span>
                                <a href="${article.link}" target="_blank" class="text-amber-400 font-bold flex items-center gap-0.5 hover:underline">Lire la suite →</a>
                            </div>
                            `}
                        `;
                        conteneur.appendChild(card);

                        if (index === 0 && notifier) { afficherNotif(article.title); }
                    });

                    loader.classList.add('hidden');
                    conteneur.classList.remove('hidden');
                    lucide.createIcons();
                }
            } catch (e) { console.error(e); }
        }

        function afficherNotif(titre) {
            const n = document.getElementById('notif-push');
            document.getElementById('notif-texte').innerText = titre;
            n.classList.remove('translate-y-32');
            setTimeout(() => { fermerNotif(); }, 6000);
        }

        function fermerNotif() { document.getElementById('notif-push').classList.add('translate-y-32'); }
        function ouvrirPremium() { document.getElementById('modal-premium').classList.remove('hidden'); }
        function fermerPremium() { document.getElementById('modal-premium').classList.add('hidden'); }

        window.onload = () => { chargerActualites(); demarrerChrono(); };
    </script>
</body>
</html>
