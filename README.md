# eclipse-tunesien

## FTP-Deployment mit GitHub Actions

Der Workflow [deploy-ftp.yml](.github/workflows/deploy-ftp.yml) stellt die Website nach einem Push auf `main` automatisch im Testordner bereit. Ein Produktions-Deployment wird manuell über **Actions → Deploy website via FTP → Run workflow** gestartet. Dafür muss im Dropdown der Branch `main` ausgewählt werden.

Vor dem ersten Deployment unter **Settings → Secrets and variables → Actions** folgende Repository-Variablen anlegen:

| Variable | Beschreibung | Beispiel |
| --- | --- | --- |
| `FTP_SERVER` | FTP-Hostname ohne `ftp://` oder `ftps://` | `ftp.example.com` |
| `FTP_USERNAME` | FTP-Benutzername | `website-user` |
| `FTP_PROTOCOL` | Verbindungsprotokoll des Hosters (`ftps`, `ftps-legacy` oder `ftp`) | `ftps` |
| `FTP_TEST_DIR` | Zielordner für Test, mit abschliessendem `/` | `test/` |
| `FTP_PROD_DIR` | Zielordner für Produktion, mit abschliessendem `/` | `prod/` |

Das Passwort als Repository-Secret `FTP_PASSWORD` hinterlegen, nicht als Variable. Wenn möglich `ftps` verwenden: Unverschlüsseltes `ftp` überträgt Zugangsdaten nicht geschützt. Die FTP-Zielordner sollten ausschliesslich für diese Website verwendet werden, da der Deploy-Workflow Dateien im Zielordner mit dem Repository-Inhalt abgleicht.