# Yɛ w’ankasa SMTP mail sending server

## nnianim asɛm

SMTP betumi atɔ nnwuma afi cloud adetɔnfo hɔ tẽẽ, te sɛ:

* [Amazon SES SMTP na ɛyɛ adwuma](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali mununkum email piapia](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Wubetumi nso ayɛ w'ankasa mail server - a anohyeto nni mu a wode bɛmena, ɛho ka nyinaa sua.

Wɔ aseɛ ha yi, yɛkyerɛ anammɔn anammɔn sɛdeɛ yɛbɛkyekyere yɛn ankasa mail server.

## Server a wɔpaw

SMTP somfo a ɔno ankasa yɛ no hwehwɛ ɔmanfo IP a port 25, 456, ne 587 abue.

Ɔmanfo mununkum a wɔtaa de di dwuma no asiw saa hyɛn gyinabea ahorow yi kwan default so, na ebia ɛbɛyɛ yiye sɛ wobebue denam adwuma ho ahyɛde a wɔde bɛma so, nanso ɛyɛ ɔhaw kɛse wɔ ne nyinaa akyi.

Mekamfo kyerɛ sɛ tɔ fi host a ɛwɔ saa ports yi a wɔabue na ɛboa ma wɔhyehyɛ reverse domain names.

Ɛha yi, mekamfo [Contabo](https://contabo.com) kyerɛ.

Contabo yɛ hosting provider a ɛwɔ Munich, Germany, a wɔde sii hɔ wɔ afe 2003 mu a ne bo yɛ den yiye.

Sɛ wopaw Euro sɛ sika a wode bɛtɔ a, ne bo bɛyɛ mmerɛw (server a ɛwɔ 8GB memory ne 4 CPUs bo bɛyɛ 529 yuan afe biara, na mfitiaseɛ instɔlehyɛn ho ka no yɛ kwa afe baako).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Sɛ woreyɛ order a, remark `prefer AMD` , na server a ɛwɔ AMD CPU no benya adwumayɛ a eye.

Wɔ deɛ ɛdidi soɔ yi mu no, mɛfa Contabo VPS sɛ nhwɛsoɔ de akyerɛ sɛdeɛ wobɛkyekyere w’ankasa mail server.

## Ubuntu nhyehyɛe nhyehyɛe

Dwumadi nhyehyɛe a ɛwɔ ha ne Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Sɛ server a ɛwɔ ssh so no kyerɛ a `Welcome to TinyCore 13!` (sɛnea wɔakyerɛ wɔ mfonini a ɛwɔ ase ha no mu no), ɛkyerɛ sɛ wonnya nhyehyɛɛ nhyehyɛe no. Yɛsrɛ wo, twa ssh no mu na twɛn simma kakraa bi na woasan akɔ mu bio.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Sɛ `Welcome to Ubuntu 22.04.1 LTS` pue a, mfitiaseɛ no awie, na wobɛtumi akɔ so ayɛ anammɔn a ɛdidi soɔ yi.

### [Optional] Fi ase nkɔso tebea no

Saa anammɔn yi yɛ nea obiara betumi apaw.

Sɛnea ɛbɛyɛ a ɛbɛyɛ mmerɛw no, mede ubuntu softwea no instɔlehyɛn ne nhyehyɛe nhyehyɛe no too [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Run ahyɛde a edidi so yi na fa klike biako install.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Chinafoɔ a wɔde di dwuma, yɛsrɛ sɛ fa ahyɛdeɛ a ɛdidi soɔ yi di dwuma mmom, na kasa, berɛ fã, ne nea ɛkeka ho no bɛhyehyɛ no ara.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo ma IPV6 tumi yɛ adwuma

Ma IPV6 nyɛ adwuma sɛnea ɛbɛyɛ a SMTP nso betumi de email ahorow a IPV6 address wom amena.

siesie / ne nea ɛkeka ho `/etc/sysctl.conf`

Sesa anaa fa nkyerɛwde a edidi so yi ka ho

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Di [contabo nkyerɛkyerɛ no akyi: IPv6 nkitahodi a wode bɛka wo server no ho](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Edit `/etc/netplan/01-netcfg.yaml` , fa nkyerɛwde kakraa bi ka ho sɛnea wɔakyerɛ wɔ mfonini a ɛwɔ ase ha no mu (Contabo VPS default configuration file no wɔ saa nkyerɛwde yi dedaw, yi nsɛm fi mu kɛkɛ).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Afei `netplan apply` na ama nhyehyeɛ a wɔasesa no ayɛ adwuma.

Sɛ nhyehyeɛ no di yie wie a, wobɛtumi de `curl 6.ipw.cn` adi dwuma de ahwɛ wo abɔnten ntwamutam no ipv6 address.

## Clone nhyehyeɛ akoraeɛ ops

```
git clone https://github.com/wactax/ops.soft.git
```

## Yɛ SSL abodin krataa a wontua hwee ma wo domain din

Sɛ wode mail bɛmena a, ɛhia SSL abodin krataa ma encryption ne signing.

Yɛde [acme.sh](https://github.com/acmesh-official/acme.sh) di dwuma de yɛ adansedi nkrataa.

acme.sh yɛ adwinnade a wɔde wɔn nsa hyɛ ase a wɔde di dwuma wɔ ɔkwan a ɛyɛ adwuma so a wɔde di dwuma wɔ ɔkwan a ɛyɛ adwuma so, .

Hyehyɛ nhyehyeɛ adekorabea ops.soft, tu mmirika `./ssl.sh` , na wɔbɛbɔ `conf` folda wɔ **soro daerekta no** mu .

Hwehwɛ wo DNS dwumadiefoɔ no firi [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , sesa `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Afei tu mmirika `./ssl.sh 123.com` na yɛ `123.com` ne `*.123.com` adansedi nkrataa ma wo domain din.

Mmirikatuo a ɛdi kan no bɛhyehyɛ [acme.sh](https://github.com/acmesh-official/acme.sh) no ara na ɛde adwuma a wɔahyɛ da ayɛ ama foforɔyɛ a ɛyɛ ne ho bɛka ho. Wubetumi ahu `crontab -l` , nkyerɛwde a ɛte saa wɔ hɔ sɛnea edidi so yi.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Ɔkwan a wɔfa so de abodin krataa a wɔayɛ no yɛ biribi te sɛ `/mnt/www/.acme.sh/123.com_ecc。`

Abodin krataa foforɔ bɛfrɛ `conf/reload/123.com.sh` script, sesa saa script yi, wobɛtumi de ahyɛdeɛ te sɛ `nginx -s reload` ho de ayɛ abodin krataa cache a ɛwɔ application a ɛfa ho no foforɔ.

## Yɛ SMTP server ne chasquid

[chasquid](https://github.com/albertito/chasquid) yɛ SMTP server a wɔabue ano a wɔakyerɛw wɔ Go kasa mu.

Sɛ́ nea wɔde besi tete mail server nhyehyɛe ahorow te sɛ Postfix ne Sendmail ananmu no, chasquid yɛ mmerɛw na ɛnyɛ den sɛ wɔde bedi dwuma, na ɛyɛ mmerɛw nso ma nkɔso a ɛto so abien.

Run `./chasquid/init.sh 123.com` bɛhyehyɛ no ankasa wɔ klike biako so (fa wo domain din a wode remena no si 123.com ananmu).

## Hyehyɛ Email Nsaano Nkyerɛwee DKIM

Wɔde DKIM di dwuma de email nsaano nkyerɛwee mena de siw nkrataa a wɔremfa nni dwuma sɛ spam.

Sɛ ahyɛdeɛ no kɔ yie a, wɔbɛka akyerɛ wo sɛ hyehyɛ DKIM kyerɛwtohɔ no (sɛnea wɔakyerɛ wɔ aseɛ ha yi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Fa TXT kyerɛwtohɔ bi ka wo DNS ho kɛkɛ (sɛnea wɔakyerɛ wɔ ase ha no).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Hwɛ ɔsom tebea & logs

 `systemctl status chasquid` Hwɛ ɔsom tebea.

Tebea a ɛwɔ oprehyɛn a ɛfata mu no te sɛ nea wɔakyerɛ wɔ mfonini a ɛwɔ ase ha no mu

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` anaa `journalctl -xeu chasquid` betumi ahwɛ mfomso kyerɛwtohɔ no.

## Dane domain din nhyehyɛe no akyi

Domain din a ɛdannan no ne sɛ ɛbɛma kwan ma wɔasiesie IP address no akɔ domain din a ɛne no hyia no so.

Sɛ wode reverse domain name si hɔ a, ebetumi asiw email ahorow ano sɛ wɔrenhu sɛ ɛyɛ spam.

Sɛ wɔgye mail no a, server a ɛregye no bɛyɛ reverse domain name analysis wɔ IP address a ɛwɔ server a ɛde remena no so de si so dua sɛ server a ɔde remena no wɔ reverse domain din a ɛfata anaa.

Sɛ server a ɔde remena no nni reverse domain din anaasɛ reverse domain din no ne IP address a ɛwɔ server a ɔde remena no mu no nhyia a, server a ɛregye no betumi ahu email no sɛ spam anaasɛ ɔbɛpow.

Kɔ [https://my.contabo.com/rdns](https://my.contabo.com/rdns) na hyehyɛ sɛnea wɔakyerɛ wɔ aseɛ ha yi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Sɛ wohyehyɛ reverse domain din no wie a, kae sɛ wobɛhyehyɛ forward resolution a ɛwɔ domain din ipv4 ne ipv6 no so akɔ server no so.

## Sesa hostname a ɛwɔ chasquid.conf no

Sesa `conf/chasquid/chasquid.conf` ma ɛnyɛ domain din a ɛdannan no boɔ.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Afei run `systemctl restart chasquid` na san hyɛ ɔsom no ase.

## Backup conf kɔ git akoraeɛ

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Sɛ nhwɛsoɔ no, me backup conf folder no kɔ m’ankasa github process so sɛdeɛ ɛdidi soɔ yi

Di kan yɛ kokoam adekoradan

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Hyehyɛ conf directory no mu na fa kɔ warehouse no mu

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Fa nea ɔde kɔmaa no ka ho

dwane

```
chasquid-util user-add i@wac.tax
```

Wobetumi de nea ɔde kɔmaa no aka ho

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Hwɛ sɛ wɔahyehyɛ password no yiye

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Sɛ wode ɔdefoɔ no ka ho wie a, `chasquid/domains/wac.tax/users` bɛyɛ foforɔ, kae sɛ wode bɛkɔ adekoradan no mu.

## DNS de SPF kyerɛwtohɔ ka ho

SPF ( Sender Policy Framework ) yɛ mfiridwuma a wɔde di email mu nokware a wɔde siw email nsisi ano.

Ɛhwɛ sɛ obi a ɔde nkrataa mena no yɛ nokware denam hwɛ a ɛhwɛ sɛ nea ɔde nkrataa mena no IP address ne domain din a ɔkyerɛ sɛ ɛyɛ no DNS kyerɛwtohɔ ahorow hyia, na ɛmma nsisifo ntumi mfa atoro email nkɔma.

SPF kyerɛwtohɔ ahorow a wode bɛka ho no betumi asiw email ahorow a wɔbɛkyerɛ sɛ ɛyɛ spam sɛnea ɛbɛyɛ yiye biara.

Sɛ wo domain din server no ntumi mmoa SPF type a, fa TXT type record ka ho kɛkɛ.

Sɛ nhwɛso no, SPF a ɛwɔ `wac.tax` mu no te sɛ nea edidi so yi

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF ma `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Hyɛ no nsow sɛ mewɔ `include:_spf.google.com` wɔ ha, eyi te saa efisɛ mɛhyehyɛ `i@wac.tax` sɛ address a wɔde bɛmena wɔ Google mailbox no mu akyiri yi.

## DNS nhyehyeɛ DMARC

DMARC yɛ (Domain-based Message Authentication, Reporting & Conformance) a wɔatwa no tiaa.

Wɔde kyere SPF bounces (ebia ɛnam nhyehyeɛ mfomsoɔ nti, anaasɛ obi foforɔ reyɛ ne ho sɛ wo na wode spam amena).

Fa TXT kyerɛwtohɔ `_dmarc` , .

Nsɛm a ɛwɔ mu no te sɛ nea edidi so yi

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Parameter biara asekyerɛ te sɛ nea edidi so yi

### p (Nhyehyɛe) .

Kyerɛ sɛnea wobedi email ahorow a entumi nyɛ SPF (Sender Policy Framework) anaa DKIM (DomainKeys Identified Mail) nokwaredi ho dwuma. Wobetumi de p parameter no ahyɛ botae abiɛsa no mu biako so:

* biara nni hɔ: Wɔnnyɛ ade biara, nea efi mu ba a ɛkyerɛ sɛ ɛyɛ nokware no nkutoo na wɔde ma nea ɔde kɔmaa no denam email amanneɛbɔ kwan no so.
* Quarantine: Fa mail a ɛntwam verification no kɔ spam folda no mu, nanso ɛrempow mail no tẽẽ.
* pow: Pow email ahorow a entumi nnye nokware no tẽẽ.

### fo (Nneɛma a Wɔde Di Dwuma) .

Kyerɛ nsɛm dodow a amanneɛbɔ nhyehyɛe no de bɛsan aba. Wobetumi de ahyɛ nneɛma a edidi so yi mu biako so:

* 0: Bɔ validation aba ho amanneɛ ma nkrasɛm nyinaa
* 1: Bɔ nkrasɛm a entumi nyɛ nokware nkutoo ho amanneɛ
* d: Bɔ domain din nokwaredi a entumi nyɛ yiye nkutoo ho amanneɛ
* s: bɔ SPF nokwaredi huammɔdi nkutoo ho amanneɛ
* l: Bɔ DKIM nokwaredi huammɔdi nkutoo ho amanneɛ

### rua & ruf

* rua (URI a wɔde ma amanneɛbɔ a wɔaboaboa ano): Email address a wɔde gye amanneɛbɔ a wɔaboaboa ano
* ruf (URI a wɔde bɔ amanneɛ ma Forensic amanneɛbɔ): email address a wode begye amanneɛbɔ a ɛkɔ akyiri

## Fa MX kyerɛwtohɔ ahorow ka ho na fa email ahorow kɔ Google Mail

Esiane sɛ mantumi anhu adwumakuw mailbox a wontua hwee a ɛboa amansan address ahorow (Catch-All, ebetumi anya email biara a wɔde akɔ domain din yi so, a anohyeto biara nni mu wɔ prefixes ho), mede chasquid dii dwuma de email nyinaa kɔɔ me Gmail mailbox so.

**Sɛ wowɔ w’ankasa adwuma mailbox a wotua ho ka a, yɛsrɛ wo nsakra MX no na twa anammɔn yi so.**

Sesa `conf/chasquid/domains/wac.tax/aliases` , hyehyɛ nkrataa adaka a wɔde bɛkɔ

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` kyerɛ email nyinaa, `i` yɛ email address prefix a ɔde soma ɔdefo a wɔayɛ wɔ atifi hɔ no. Sɛ wode mail bɛkɔ a, ɛsɛ sɛ obiara a ɔde di dwuma no de line bi ka ho.

Afei fa MX kyerɛwtohɔ no ka ho (metwe adwene si address a ɛwɔ reverse domain name no so tẽẽ wɔ ha, sɛnea wɔakyerɛ wɔ line a edi kan wɔ mfonini a ɛwɔ ase ha no mu no).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Sɛ nhyehyeɛ no wie a, wobɛtumi de email address foforɔ adi dwuma de email akɔ `i@wac.tax` ne `any123@wac.tax` de ahwɛ sɛ wobɛtumi anya email wɔ Gmail mu anaa.

Sɛ ɛnte saa a, hwɛ chasquid log ( `grep chasquid /var/log/syslog` ).

## Fa email mena i@wac.tax denam Google Mail so

Bere a Google Mail nsa kaa mail no akyi no, sɛnea ɛte no, na mewɔ anidaso sɛ mede `i@wac.tax` bebua sen sɛ mede i.wac.tax@gmail.com bebua.

Kɔ [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) na klik "Fa email address foforo ka ho".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Afei, kyerɛw verification code a email a wɔde kɔmaa no no nsa aka no.

Awiei koraa no, wobetumi de asi hɔ sɛ address a wɔde amena no (a ɛka ho ne ɔkwan a wobɛfa so de address koro no ara abua).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Saa kwan yi so no, yɛawie SMTP mail server no a yɛde besi hɔ na bere koro no ara mu no yɛde Google Mail di dwuma de mena na yɛgye email.

## Fa sɔhwɛ email mena na hwɛ sɛ nhyehyɛe no adi nkonim anaa

Hyehyɛ `ops/chasquid`

Run `direnv allow` ma instɔlehyɛn dependencies (wɔde direnv ahyɛ mu wɔ kan one-key initialization process no mu na wɔde hook aka shell no ho)

afei tu mmirika

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Nkyerɛase a ɛwɔ parameters no mu ne nea edidi so yi

* ɔdefoɔ: SMTP dwumadie din
* pass: SMTP asɛmfua a wɔde hyɛ mu
* to: nea ogye no

Wubetumi de sɔhwɛ email amena.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Wɔhyɛ nyansa sɛ fa Gmail di dwuma de gye sɔhwɛ email ahorow de hwɛ sɛ nhyehyɛe ahorow no adi nkonim anaa.

### TLS gyinapɛn encryption

Sɛnea wɔakyerɛ wɔ mfonini a ɛwɔ aseɛ ha yi mu no, saa lock ketewa yi wɔ hɔ, a ɛkyerɛ sɛ wɔama SSL abodin krataa no ayɛ adwuma yie.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Afei klik "Kyerɛ Original Email".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Sɛnea wɔakyerɛ wɔ mfonini a ɛwɔ aseɛ ha yi mu no, Gmail mfitiaseɛ mail krataafa no bɛkyerɛ DKIM, a ɛkyerɛ sɛ DKIM nhyehyeɛ no adi nkonim.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Hwɛ Received wɔ email a edi kan no ti mu, na wobɛtumi ahunu sɛ address a ɔde amena no yɛ IPV6, a ɛkyerɛ sɛ wɔahyehyɛ IPV6 nso yie.
