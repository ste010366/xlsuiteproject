# XLSuite Project – portale

Sito statico (HTML/CSS) del portale con il marchio comune e i collegamenti ai tre prodotti:
XLSuite Volley, XLSuite Soccer, XLSuite Basket. Dominio: **xlsuiteproject.it**.

File: `index.html`, `style.css`, `img/` (icone dei tre Club), `CNAME`, `.nojekyll`.

## Prova in locale
```
python -m http.server 8080
```
poi apri http://localhost:8080

## Pubblicazione su GitHub Pages (stesso schema di xlsuitevolley.it)
1. **Repo**: su GitHub crea un repository, es. `xlsuiteproject` (pubblico, vuoto).
2. **Push**: dalla cartella del sito
   ```
   git init
   git add .
   git commit -m "Portale XLSuite Project"
   git branch -M main
   git remote add origin https://github.com/<ACCOUNT>/xlsuiteproject.git
   git push -u origin main
   ```
3. **Pages**: Settings → Pages → *Build and deployment*: Source = *Deploy from a branch*, Branch = `main`, cartella `/ (root)`.
4. **Dominio**: sempre in Settings → Pages → *Custom domain* inserisci `xlsuiteproject.it` e salva (il file `CNAME` lo fa già in automatico al push).
5. **DNS su Aruba** (Pannello → Gestione DNS di xlsuiteproject.it). Elimina eventuali record A/AAAA/CNAME preesistenti per `@` e `www`, poi aggiungi:

   | Tipo | Nome | Valore |
   |---|---|---|
   | A | `@` | 185.199.108.153 |
   | A | `@` | 185.199.109.153 |
   | A | `@` | 185.199.110.153 |
   | A | `@` | 185.199.111.153 |
   | CNAME | `www` | `<ACCOUNT>.github.io.` |

   (Facoltativo, per IPv6: record AAAA `@` → 2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153, 2606:50c0:8003::153. Se Aruba offre un record ALIAS/ANAME per `@`, si può usare verso `<ACCOUNT>.github.io` al posto dei quattro A.) Verifica gli IP aggiornati nella documentazione GitHub Pages.
6. **Attesa**: la propagazione DNS richiede da pochi minuti a qualche ora. Quando GitHub riconosce il dominio (segno di spunta verde in Settings → Pages), il certificato Let's Encrypt viene emesso in automatico (fino a ~1 ora, a volte più).
7. **HTTPS**: a certificato pronto, spunta *Enforce HTTPS*. Poi prova https://xlsuiteproject.it e https://www.xlsuiteproject.it (quest'ultimo reindirizza al dominio principale).

Se il dominio non viene accettato, controlla i record con `nslookup xlsuiteproject.it` e che nessun altro repo usi lo stesso dominio.
