# AD
Logonscript:
$CompName = get-content ENV:ComputerName
$UserName = get-content ENV:UserName
$Date = get-date -Format "dd-MM-yyyy HH:mm"
$FileName = get-date -Format yyyyMM
$IPAddress = Get-NetIPAddress -IPAddress 10.0.6.*|Select-Object -ExpandProperty IPaddress
$Text = "Logon: " + $UserName + " " + $CompName + " " + $Date + " " + $IPAddress
$Text|Out-File -Append -FilePath C:\USERS\ProCoder\Documents\$Filename.txt
////////////////////////////////////////////////////////////////////////////////
4.1
Clear-Host
[int]$number1 = Read-Host "geef het eerste getal in"
[int] $number2= Read-Host "geef het tweede getal in"
[int] $verschil= $number1 - $number2
[int] $som = $number1 + $number2
[int] $product = $number1 * $number2
[double] $quotient = $number1 / $number2

 " het verschil tussen $number1 en $number2 is $verschil"
 " de som tussen $number1 en $number2 is $som"
 " het product tussen $number1 en $number2 is $product"
 " het quotient tussen $number1 en $number2 is $quotient"
 ////////////////////////////////////////////////////////////////////////////////
4.3
$set1 = (Get-Date).AddDays(-10)
$set2 = (Get-Date).AddDays(-20)
$set3 = (Get-Date).AddDays(-30)
$set4 = (Get-Date).AddDays(-40)

#$dagen = Write-Host "geef het aantal dagen in"

Get-Item C:\data1\file_?.txt | foreach-object {$_.Creationtime = $set1}
Get-Item C:\data1\file_1?.txt | foreach-object {$_.Creationtime = $set2}
Get-Item C:\data1\file_2?.txt | foreach-object {$_.Creationtime = $set3}
Get-Item C:\data1\file_3?.txt | foreach-object {$_.Creationtime = $set4}

$days = (Get-Date).AddDays(-20)
Get-ChildItem -Path C:\data1 -Recurse -Force | where-object {!$_.PSIscontainer -and $_.CreationTime -lt $days} | Remove-Item

$tdc='C:\data1'
$a = Get-ChildItem $tdc -recurse | Where-Object {$_.PSIsContainer -eq $True}
$a | Where-Object {$_.GetFiles().Count -eq 0} | Remove-Item
////////////////////////////////////////////////////////////////////////////////
7.3
New-ADGroup -GroupScope Global -Name Sales -Path "ou=Sint-Niklaas, dc=MediaTech, dc=lan"
Move-ADObject -TargetPath "Group=Sales, ou=Sint-Niklaas, dc=MediaTech, dc=lan"
Set-ADUser -Identity BEP -Department Sales
Add-ADGroupMember -Identity IT -Members BEP
////////////////////////////////////////////////////////////////////////////////
7.2
New-ADOrganizationalUnit -Name Sint-Niklaas
New-ADGroup -Name IT -Path "ou=Sint-Niklaas, DC=mediatech, DC=lan"
Add-ADGroupMember -Identity IT-Members bep
////////////////////////////////////////////////////////////////////////////////
7.1
Set-ADUser -Identity ll-72960 -Company Mediatech -Department IT -EmailAddress proCoder@outlook.com
Get-ADuser -Identity ll-72960 -Properties *|format-table emailaddress,company,department

////////////////////////////////////////////////////////////////////////////////


$users = Import-Csv -Delimiter ";" -path c:\Import_ADUsers.csv
ForEach($user in $users)
{
$fullname = $user.firstname + " " + $user.lastname
$firstname = $user.firstname
$lastname = $user.lastname
$domain = "@mediatech.lan"
$upn = $user.lastname + $domain
$ou = $user.oud
$password = $user.password
$driveletter = "H:"
$homefolder = $user.homefolder
$setpassword = ConvertTo-SecureString $password -AsPlainText -Force
}
////////////////////////////////////////////////////////////////////////////////

New-ADUser -name $fullname
 -DisplayName $fullname
  -GivenName $firstname 
  -surname $lastname 
  -SamAccountName $user.lastname 
  -HomeDrive $driveletter
-HomeDirectory $homefolder 
-UserPrincipalName $UPN 
-path $ou
 -AccountPassword $setpassword 
 -enabled $true -passThru

////////////////////////////////////////////////////////////////////////////////
Clear-Host
[int]$getal = Read-Host "kies een getal tussen 1 en 5"
Switch ($getal)
{
2 {Write-Host "u heeft het nummer 2 gekozen"}
3 {Write-Host "u heeft het nummer 3 gekozen"}
4 {Write-Host "u heeft het nummer 4 gekozen"}
5 {Write-Host "u heeft het nummer 5 gekozen"}
}
////////////////////////////////////////////////////////////////////////////////
Clear-Host
[int]$getal = 0
do{
write-host "de waarde van het getal is $getal"
$getal++

}
while($getal -lt 10)


////////////////////////////////////////////////////////////////////////////////

Clear-Host
for([int] $a = 0; $a -lt 11; $a++){
write-host "de waarde van '$a is $a"
}

////////////////////////////////////////////////////////////////////////////////

Clear-Host
[int] $leeftijd = Read-Host "geef je leeftijd in: "

if($leeftijd -lt 16) {
Write-Host "Je bent jonger dan 16" ;break
}
if($leeftijd -lt 25) {
Write-Host "Je bent jonger dan 25" ;break
}
if($leeftijd -lt 40) {
Write-Host "Je bent jonger dan 40" ;break
}
if($leeftijd -gt 40) {
Write-Host "Je bent ouder dan 40" ;break
}
