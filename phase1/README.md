# HE簡易判定 Phase 1（試作・単一HTML）

ブラウザだけで動く Happy Eyeballs 簡易判定ページ。ビルド不要、`index.html` 1ファイル。

## 公開手順（GitHub Pages）

1. GitHubで新規リポジトリ作成（Public推奨、README付きで可）
2. この `index.html` をリポジトリ直下に配置してpush
   - 例: `git init / branch -M main / add / commit / remote add origin ... / push -u origin main`
3. リポジトリの **Settings → Pages → Build and deployment → Deploy from a branch**、
   Branchを `main` / `(root)` にしてSave
4. 数十秒〜数分で `https://<user>.github.io/<repo>/` が公開される
5. **Enforce HTTPS** がONであることを確認（測定先が全てHTTPSのため必須）

この手順で問題ありません。単一静的ファイルなのでActionsは不要です。

## ローカル確認

```powershell
cd phase1
python -m http.server 8080
# http://localhost:8080/ を開く（file:// 直開きでも概ね動きますが推奨しません）
```

## 使っている外部エンドポイント（要CORSのものは代替付き）

- 既定egress: api64.ipify.org / cloudflare trace / wtfismyip
- v4固定: ipv4.icanhazip.com / v4.ident.me / ipinfo.io
- v6固定: ipv6.icanhazip.com / v6.ident.me / ipv6.seeip.org
- 初回計測: google/gstatic generate_204, cloudflare trace, captive.apple.com, detectportal
- 逆引き: dns.google (DoH)

## 既知の制限（Phase 2送り）

- TCP相内訳・ファミリ別スループット（自前EP＋ワイルドカードDNS＋TAOが必要）
- PPPoE/IPoEの断定（ブラウザからは不可、推定表示のみ）
