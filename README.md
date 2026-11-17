// ==UserScript==
// @name         GitHub Logo Değiştirici
// @namespace    http://tampermonkey.net
// @version      1.0
// @description  GitHub kedi logosunu özel bir logo ile değiştirir.
// @author       You
// @match        https://github.com*
// @grant        none
// @run-at       document-end
// ==/UserScript==

(function() {
    'use strict';

    // KULLANIM: Alttaki tırnak içine koymak istediğiniz logonun internet linkini (URL) yapıştırın.
    const yeniLogoUrl = "https://picsum.photos"; 

    function logoyuDegistir() {
        // Sol üstteki kedi logosunu içeren SVG elementini bulur
        const kediLogosu = document.querySelector('header svg.octicon-mark-github, div svg.octicon-mark-github');
        
        if (kediLogosu) {
            // Yeni bir resim elementi oluşturur
            const yeniLogo = document.createElement('img');
            yeniLogo.src = yeniLogoUrl;
            yeniLogo.style.width = '32px';
            yeniLogo.style.height = '32px';
            yeniLogo.style.borderRadius = '50%'; // Yuvarlak yapmak isterseniz
            yeniLogo.style.objectFit = 'contain';

            // Eski logoyu silip yenisini ekler
            kediLogosu.parentNode.replaceChild(yeniLogo, kediLogosu);
        }
    }

    // Sayfa ilk yüklendiğinde çalıştır
    logoyuDegistir();

    // GitHub dinamik sayfa geçişleri yaptığı için logoyu düzenli aralıklarla kontrol et
    setInterval(logoyuDegistir, 1000);
})();
