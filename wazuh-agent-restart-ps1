# Ensure-WazuhAgent.ps1
# Controlla lo stato del servizio Wazuh Agent e lo avvia se non è in esecuzione.

$ServiceNames = @("WazuhSvc","ossecsvc")   # WazuhSvc è il più comune; ossecsvc per vecchie installazioni

$svc = $null
foreach ($name in $ServiceNames) {
    $svc = Get-Service -Name $name -ErrorAction SilentlyContinue
    if ($svc) { break }
}

if (-not $svc) {
    exit 2  # servizio non trovato
}

$svc.Refresh()

if ($svc.Status -ne "Running") {
    try {
        Start-Service -Name $svc.Name -ErrorAction Stop
        exit 0
    }
    catch {
        exit 1
    }
}

exit 0
