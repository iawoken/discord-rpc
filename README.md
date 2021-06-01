# Özel Discord RPC

Bu dökümanı okuyarak, discord'da kendinize özel bir RPC durum ayarlayabilirsiniz!

### Gerekenler
* Discord'a Masaüstü üzerinden giriş yapmanız gerekmektedir. (Mobil veya WEB tarayıcı ile giriş yapmak sayılmaz.)
* [NodeJS](https://nodejs.org/en/download/) (İhtiyaç duyulan modülleri içerisinde barındırıyor.)

## Birinci Adım: Uygulamamızı Oluşturalım
* [Developer Portal](https://discord.com/developers/applications)'a giriş yapın ardından > "New Application" butonuna tıklayın.
* Uygulama ismini belirtin. (Buraya girdiğiniz isim RPC Durumundaki isminiz olacaktır.)
* Rich Presence > Art Assets sekmesine girin, bir resim yükleyin (isteğe bağlı) ve bu adı bir yere not edin (lazım olacak.)

## İkinci Adım: Projemizi Oluşturalım
* Yeni bir klasör oluşturun ve ardından bu klasörü kod editörünüz ile birlikte açın.
* Projenizde bir komut terminali açın ve `npm init -y` komutunu girin. Böylelikle package.json dosyamızı oluşturduk. (Eğer hata alırsanız: `npm init` komutu ile kurmayı deneyin.)
* Ardından `discord-rpc` modülünü kurun. (`npm install discord-rpc`) 
* Şimdi bir index.js dosyası oluşturun ve aşağıdakileri kodları ekleyin:
```js
const RPC = require('discord-rpc');
const client = new RPC.Client({
    transport: 'ipc'
});

client.on('ready', () => {
    client.request('SET_ACTIVITY', {
        pid: process.pid,
        activity: {
            details: "Detaylar buraya",
            state: "State kısmı buraya",
            timestamps: {
                start: Date.now()
            },
            assets: {
                large_image: "", // "Developer Portal > Application > Rich Presence" kısmına eklediğiniz resimin anahtarını girin.
                large_text: "buyuk resim yazi" // "Rich Presence" alanına eklediğiniz resmin ismini belirtin.
            },
            buttons: [
                { label: "Buton 1", url: "https://github.com/iawoken" },
                { label: "Buton 2", url: "https://github.com/iawoken" }
            ]
        }
    });
});

client.login({
    clientId: '', // Uygulamanızın ID'sini buraya girin.
    clientSecret: '' // "Client Secret" anahtarını buraya girin.
});
```

## Üçüncü Adım: RPC'yi Başlatma
* Tüm dosyaları kaydedin, ardından `node index.js` komutunu komut satırına yazın.
* Uygulama başlatıldığında profilinizde bu şahane durum gözükür olacaktır.
