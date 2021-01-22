<?
define("STOP_STATISTICS",true);
define("NO_KEEP_STATISTIC",'Y');
define("NO_AGENT_STATISTIC",'Y');
define("NO_AGENT_CHECK",true);
define("DisableEventsCheck",true);
require_once($_SERVER["DOCUMENT_ROOT"]."/bitrix/modules/main/include/prolog_before.php");
// Сперва на сервере используется HTTP Basic авторизация, выполняем ее:
$url = "/authenticate";
$ch = curl_init();
curl_setopt($ch,CURLOPT_RETURNTRANSFER,1);
curl_setopt($ch,CURLOPT_URL,$url);
curl_setopt($ch,CURLOPT_USERPWD,"****@mail.ru:*****");
$result = curl_exec($ch);
curl_close($ch);
//echo $result;
//В случае удачной авторизации выводится веб-форма, куда нужно забить следующую пару логин/пароль
function read($url){
	$ch = curl_init();
	curl_setopt($ch,CURLOPT_URL,$url);
	curl_setopt($ch,CURLOPT_REFERER,$url);
	curl_setopt($ch,CURLOPT_POST,0);
	curl_setopt($ch,CURLOPT_FOLLOWLOCATION,1);
	curl_setopt($ch,CURLOPT_COOKIEFILE,$_SERVER['DOCUMENT_ROOT'].'/test/cookie.txt');
	curl_setopt($ch,CURLOPT_USERAGENT,"Mozilla/4.0 (Windows; U; Windows NT 5.0; En; rv:1.8.0.2) Gecko/20070306 Firefox/1.0.0.4");
	$result = curl_exec($ch);
	curl_close($ch);
	return $result;
}
read('.xml?q=MOEX');
//require_once($_SERVER["DOCUMENT_ROOT"].BX_ROOT."/modules/main/include/epilog_after.php");
