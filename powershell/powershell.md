# PowerShell

## コマンドレット

- コマンドの場所：Get-Command ssh
- grep 的な：Select-String
- eval 的な : Invoke-Expression

## その他

- 環境変数設定  
  \$env:変数名 = "aaaa"
- 環境変数再読み込み  
  \$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
