<h1>杜甫全集注本、杜甫資料庫</h1>
<h2>兩個關於杜甫詩文的儲存庫（Repositories）</h2>
<ul>
<li>杜甫全集、注本之原始資料</li>
<li>杜甫詩分析、資料庫（JSON)</li>
</ul>
<h2>指導原則</h2>
<ul>
<li>MVC 模式</li>
<li>只儲存原始資料、基於原始資料而生成之 JSON 資料庫（model），以及生成資料、生成面貌（views）之 PHP、 Python 程式 （controller），而不儲存面貌文檔（少量樣本除外）</li>
<li>以基底正文樹（base-text trees）、後設資料，共同生成面貌（views）</li>
<li>還原某版本、某注本原來之模樣，如《全唐詩》之杜甫部分，屬於生成面貌（views）之層次</li>
<li>原始資料附帶後設資料（metadata）標記</li>
<li>Controller 亦生成 meta-metadata：後設資料標記之索引、分類</li>
<li>杜甫詩文搜索采用樹路徑算法</li>
<li>樹路徑體現爲坐標；坐標集乃一封閉系統，可盡數羅列</li>
</ul>

<h2>基底正文樹</h2>
<p>基底正文樹爲儲存杜詩之樹結構，基底正文指規範化後之杜詩默認版本。例（0013《題張氏隱居二首》其一）：</p>
<pre>
"0013-1":
	"副題": "其一"
	"5":
		"1":
			"1": "春"
			"2": "山"
			"3": "無"
			"4": "伴"
			"5": "獨"
			"6": "相"
			"7": "求"
		"2":
			"1": "伐"
			"2": "木"
			"3": "丁"
			"4": "丁"
			"5": "山"
			"6": "更"
			"7": "幽"
	"6":
		"1":
			"1": "澗"
			"2": "道"
			"3": "餘"
			"4": "寒"
			"5": "歷"
			"6": "冰"
			"7": "雪"
		"2":
			"1": "石"
			"2": "門"
			"3": "斜"
			"4": "日"
			"5": "到"
			"6": "林"
			"7": "丘"
	"7":
		"1":
			"1": "不"
			"2": "貪"
			"3": "夜"
			"4": "識"
			"5": "金"
			"6": "銀"
			"7": "氣"
		"2":
			"1": "遠"
			"2": "害"
			"3": "朝"
			"4": "看"
			"5": "麋"
			"6": "鹿"
			"7": "遊"
	"8":
		"1":
			"1": "乘"
			"2": "興"
			"3": "杳"
			"4": "然"
			"5": "迷"
			"6": "出"
			"7": "處"
		"2":
			"1": "對"
			"2": "君"
			"3": "疑"
			"4": "是"
			"5": "泛"
			"6": "虛"
			"7": "舟"
</pre>
<p>基底正文樹之最大特點：此樹僅爲一容器；樹中之葉子（端節點），卽樹中之任何一字，均可被刪除，亦可以任何不限字數、不限語言之文字替換。（試想象以圖像、音頻之鏈接取代之。）</p>

<h2>後設資料標記</h2>
<p>後設資料標記指附於原始資料後之標記，內含坐標、類別、注者姓名、引書出處等資料。例（0001《全唐詩》）：</p>
<pre>
奉贈韋左丞丈二十二韻[韋濟。天寶七載爲河南尹。遷尙書左丞。]〘{"cat":"異","a":"1"}〙
少[一作妙]〘{"cat":"異","a":"少"}〙
卜[一作爲]〘{"cat":"異","a":"卜"}〙
出[一作生。一作特]〘{"cat":"異","a":"出"}〙
食[一作客]〘{"cat":"異","a":"食"}〙
歘〘{"cat":"異","a":"欻"}〙
鱗[天寶中。詔徵天下士有一藝者。皆得詣京師就選。李林甫抑之。奏令考試。遂無一人得第者。]〘{"cat":"異","a":"鱗"}〙
祗〘{"cat":"異","a":"祇"}〙
沒[一作波]〘{"cat":"異","a":"沒"}〙
</pre>
<p>利用基底正文樹、後設資料，可生成《全唐詩》之《奉贈韋左丞丈二十二韻》。</p>
<p>後設資料之最大優點：注本之注文與杜甫原文完全分離，所有注本共用一套基底正文，卻能生成無數版本；注文基本不帶基底正文，亦無號碼聯係，且不同注者之注文可同時混雜一處，互不干擾。</p>


<h2>坐標</h2>
<p>貫穿整個資料庫之搜索鍵乃一坐標系統。例：</p>
<ul>
<li>默認版本： <code>〚0003:〛</code>指《望嶽》</li>
<li>默認版本： <code>〚3789:2:〛</code>指《秋興八首》其二</li>
<li>默認版本： <code>〚0003:3.1.2〛</code>指《望嶽》中第三行第一句第二字「宗」</li>
<li>注本：<code>〚郭0001:〛</code>指郭知達《新刊校定集注杜詩》之《奉贈韋左丞丈二十二韻》</li>
<li>注本子版本：<code>〚郭⸨聶⸩ 0001:〛</code>指《新刊校定集注杜詩》聶巧平點校本《奉贈韋左丞丈二十二韻》</li>
</ul>

<h2>版本目錄（JSON）</h2>
<p>這裏亦提供重要注本之索引，包括注本之子版本之實體書、電子書頁碼、下載鏈接等。</p>
<ul>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E3%80%8A%E5%85%A8%E5%94%90%E8%A9%A9%E3%80%8B/%E5%85%A8%E7%9B%AE%E9%8C%84.json">《全唐詩》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E6%9E%97%E7%B9%BC%E4%B8%AD%E8%BC%AF%E6%A0%A1%E3%80%8A%E6%9D%9C%E8%A9%A9%E8%B6%99%E6%AC%A1%E5%85%AC%E5%85%88%E5%BE%8C%E8%A7%A3%E8%BC%AF%E6%A0%A1%E3%80%8B/%E8%B6%99%E7%9B%AE%E9%8C%84.json">林繼中輯校《杜詩趙次公先後解輯校》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E9%83%AD%E7%9F%A5%E9%81%94%E3%80%8A%E6%96%B0%E5%88%8A%E6%A0%A1%E5%AE%9A%E9%9B%86%E6%B3%A8%E6%9D%9C%E8%A9%A9%E3%80%8B/%E9%83%AD%E7%9B%AE%E9%8C%84.json">郭知達《新刊校定集注杜詩》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E8%95%AD%E6%BB%8C%E9%9D%9E%E4%B8%BB%E7%B7%A8%E3%80%8A%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86%E6%A0%A1%E6%B3%A8%E3%80%8B/%E8%95%AD%E7%9B%AE%E9%8C%84.json">蕭滌非主編《杜甫全集校注》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E7%89%88%E6%9C%AC%E7%9B%AE%E9%8C%84%E5%B0%8D%E7%85%A7%E8%A1%A8.json">版本目錄對照表</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E3%80%8A%E5%85%A8%E5%94%90%E8%A9%A9%E3%80%8B/versions/%E5%85%A8%E7%89%88%E6%9C%AC%E8%B3%87%E6%96%99.json">《全唐詩》之版本資料</a></li>
<!--
<li><a href=""></a></li>
<li></li>
<li></li>
<li></li>
-->
</ul>
<h2>杜詩（默認版本）之搜索</h2>
<p>以坐標爲主鍵，支持各種搜索。例：</p>
<ul>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/schemas/json/mapping/%E9%BB%98%E8%AA%8D%E8%A9%A9%E6%96%87%E6%AA%94%E7%A2%BC_%E8%A9%A9%E9%A1%8C.json">默文檔碼→詩題</a></li>
<li>默文檔碼→詩文</li>
<li>默詩碼→詩首句</li>
<li>同一文檔（或詩）中，出現多於一次之詩文片段（重字、重語）</li>
</ul>
<p>此等例子多屬面貌（view）層次之產物。</p>

<h2>杜注本之還原</h2>
<p>基底正文樹、後設資料標記可支持某杜注本之還原，卽此注本原書之生成。此模式最大之優點：同一基底正文樹，結合不同注本、版本之原始資料、後設資料，可生成無數之注本、版本，亦可同時展示、幷列不同注本、版本之資料。限於版權問題，只提供不受版權保護之原始資料及其後設資料。受保護之注本，如蕭滌非主編《杜甫全集校注》，則單提供後設資料。</p>
<p>注本還原亦爲面貌（view）層次之產物。</p>

<h2>面貌之多元</h2>
<p>基底正文樹、評注原始資料+後設資料標記之二元分離，可支持同一版本（如仇兆鰲之《杜詩詳註》）之五個不同面貌：</p>
<ul>
<li>以聯注（行注）形式爲主，注文插入詩文中間，卽傳統古書之面貌</li>
<li>以聯注（行注）形式爲主，注文置於詩文之後，以號碼爲聯係，如現代排版之《杜詩詳註》</li>
<li>以字注、詞注形式爲主，注文插入詩文中間，如傳統古書之讀音、異文夾注</li>
<li>以字注、詞注形式爲主，注文置於詩文之後，以號碼爲聯係，如今人之注本</li>
<li>我設計之形式，一行（或一聯）之詩文，後接該行（聯）之各種大小注文；此面貌適用於羅列不同注者之注文，評論則可散於其中，亦可置於詩文之後</li>
</ul>
<p>由於這種二元分離性，一棵《北征》之基底正文樹，配合恰當、配套之原始資料，加上對應之後設資料，可生成《北征》之英譯、日譯，甚至可以生成李白之《將進酒》，或 Harry Potter 七書中之某段文字。</p>


<!--
<h2>重要文件一覽</h2>
<h3>杜詩白文</h3>
<ul>
<li><a href="https://github.com/wingmingchan64/DuFu/blob/master/%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86.txt">杜甫全集（默認版本）</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E3%80%8A%E5%85%A8%E5%94%90%E8%A9%A9%E3%80%8B/%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86.txt">《全唐詩》杜甫卷</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E8%95%AD%E6%BB%8C%E9%9D%9E%E4%B8%BB%E7%B7%A8%E3%80%8A%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86%E6%A0%A1%E6%B3%A8%E3%80%8B/%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86.txt">蕭滌非主編《杜甫全集校注》杜詩全集</a></li>
</ul>
<h3>杜詩注音</h3>
<ul>
<li><a href="https://github.com/wingmingchan64/DuFu/blob/master/%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86%E7%B2%B5%E9%9F%B3%E6%B3%A8%E9%9F%B3.txt">杜甫全集粵音注音</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E9%99%B3%E6%B0%B8%E6%98%8E%E3%80%8A%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86%E7%B2%B5%E9%9F%B3%E6%B3%A8%E9%9F%B3%E3%80%8B/%E9%9B%99%E8%81%B2.php">雙聲</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E9%99%B3%E6%B0%B8%E6%98%8E%E3%80%8A%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86%E7%B2%B5%E9%9F%B3%E6%B3%A8%E9%9F%B3%E3%80%8B/%E7%96%8A%E9%9F%BB.php">疊韻</a></li>

</ul>
<h3>杜注目錄</h3>
<p>這些目錄，可以用來生成幾種有用的文檔，包括詩篇模板、頁碼索引等。</p>
<ul>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E6%9E%97%E7%B9%BC%E4%B8%AD%E8%BC%AF%E6%A0%A1%E3%80%8A%E6%9D%9C%E8%A9%A9%E8%B6%99%E6%AC%A1%E5%85%AC%E5%85%88%E5%BE%8C%E8%A7%A3%E8%BC%AF%E6%A0%A1%E3%80%8B/%E8%B6%99%E7%9B%AE%E9%8C%84.txt">林繼中輯校《杜詩趙次公先後解輯校》（修訂本）目錄</a></li>

<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E9%BB%83%E5%B8%8C%E3%80%81%E9%BB%83%E9%B6%B4%E3%80%8A%E9%BB%83%E6%B0%8F%E8%A3%9C%E5%8D%83%E5%AE%B6%E8%A8%BB%E7%B4%80%E5%B9%B4%E6%9D%9C%E5%B7%A5%E9%83%A8%E8%A9%A9%E5%8F%B2%E3%80%8B/%E9%BB%83%E7%9B%AE%E9%8C%84.txt">黃希、黃鶴《黃氏補千家註紀年杜工部詩史》目錄</a></li>

<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E9%83%AD%E7%9F%A5%E9%81%94%E3%80%8A%E6%96%B0%E5%88%8A%E6%A0%A1%E5%AE%9A%E9%9B%86%E6%B3%A8%E6%9D%9C%E8%A9%A9%E3%80%8B/%E9%83%AD%E7%9B%AE%E9%8C%84.txt">郭知達《新刊校定集注杜詩》目錄</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E7%8E%8B%E5%97%A3%E5%A5%AD%E3%80%8A%E6%9D%9C%E8%87%86%E3%80%8B/%E5%A5%AD%E7%9B%AE%E9%8C%84.txt">王嗣奭《杜臆》目錄</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E9%8C%A2%E8%AC%99%E7%9B%8A%E3%80%8A%E9%8C%A2%E6%B3%A8%E6%9D%9C%E8%A9%A9%E3%80%8B/%E9%8C%A2%E7%9B%AE%E9%8C%84.txt">錢謙益《錢注杜詩》目錄</a></li>

<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E6%9C%B1%E9%B6%B4%E9%BD%A1%E3%80%8A%E6%9D%9C%E5%B7%A5%E9%83%A8%E8%A9%A9%E9%9B%86%E8%BC%AF%E6%B3%A8%E3%80%8B/%E6%9C%B1%E7%9B%AE%E9%8C%84.txt">朱鶴齡《杜工部詩集輯注》目錄</a></li>

<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E4%BB%87%E5%85%86%E9%B0%B2%E3%80%8A%E6%9D%9C%E8%A9%A9%E8%A9%B3%E8%A8%BB%E3%80%8B/%E4%BB%87%E7%9B%AE%E9%8C%84.txt">仇兆鰲《杜詩詳註》目錄</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E6%A5%8A%E5%80%AB%E3%80%8A%E6%9D%9C%E8%A9%A9%E9%8F%A1%E9%8A%93%E3%80%8B/%E6%A5%8A%E7%9B%AE%E9%8C%84.txt">楊倫《杜詩鏡銓》目錄</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E6%B5%A6%E8%B5%B7%E9%BE%8D%E3%80%8A%E8%AE%80%E6%9D%9C%E5%BF%83%E8%A7%A3%E3%80%8B/%E6%B5%A6%E7%9B%AE%E9%8C%84.txt">浦起龍《讀杜心解》目錄</a></li>

<li><a href="https://github.com/wingmingchan64/DuFu/blob/master/%E7%9B%AE%E9%8C%84.txt">蕭滌非主編《杜甫全集校注》目錄</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E8%AC%9D%E6%80%9D%E7%85%92%E3%80%8A%E6%9D%9C%E7%94%AB%E9%9B%86%E6%A0%A1%E6%B3%A8%E3%80%8B/%E8%AC%9D%E7%9B%AE%E9%8C%84.txt">謝思煒《杜甫集校注》目錄</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E4%B8%8B%E5%AE%9A%E9%9B%85%E5%BC%98%E3%80%81%E6%9D%BE%E5%8E%9F%20%E6%9C%97%E3%80%8A%E6%9D%9C%E7%94%AB%E5%85%A8%E8%A9%A9%E8%A8%B3%E6%B3%A8%E3%80%8B/%E8%A8%B3%E7%9B%AE%E9%8C%84.txt">下定雅弘、松原 朗《杜甫全詩訳注》目錄</a></li>

</ul>
<h3>杜注原典文本</h3>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/tree/main/%E9%83%AD%E7%9F%A5%E9%81%94%E3%80%8A%E6%96%B0%E5%88%8A%E6%A0%A1%E5%AE%9A%E9%9B%86%E6%B3%A8%E6%9D%9C%E8%A9%A9%E3%80%8B">郭知達《新刊校定集注杜詩》卷一至卷七</a> </li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E7%8E%8B%E5%97%A3%E5%A5%AD%E3%80%8A%E6%9D%9C%E8%87%86%E3%80%8B/%E7%8E%8B%E5%97%A3%E5%A5%AD%E3%80%8A%E6%9D%9C%E8%87%86%E3%80%8B_%E5%B8%B6%E8%A9%A9%E6%96%87.txt">王嗣奭《杜臆》_帶詩文.txt</a></li>

<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E4%BB%87%E5%85%86%E9%B0%B2%E3%80%8A%E6%9D%9C%E8%A9%A9%E8%A9%B3%E8%A8%BB%E3%80%8B/%E6%9D%9C%E8%A9%A9%E8%A9%B3%E8%A8%BB%E5%8D%B7%E4%B9%8B%E4%B8%80.txt">杜詩詳註卷之一</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E4%BB%87%E5%85%86%E9%B0%B2%E3%80%8A%E6%9D%9C%E8%A9%A9%E8%A9%B3%E8%A8%BB%E3%80%8B/%E6%9D%9C%E8%A9%A9%E8%A9%B3%E8%A8%BB%E5%8D%B7%E4%B9%8B%E4%BA%8C.txt">杜詩詳註卷之二</a></li>
</ul>
<h3>資料匯總</h3>
<p>這裏儲存了一千多個以 PHP 生成的文檔，集中展示搜集來的各家注釋、評論等。隨著新資料的纍積，這些文檔也會不斷更新。</p>
<ul>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/tree/main/%E8%B3%87%E6%96%99%E5%8C%AF%E7%B8%BD">資料匯總</a></li>
<li>樣本： <a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/%E8%B3%87%E6%96%99%E5%8C%AF%E7%B8%BD/3789.txt">《秋興八首》</a></li>
<li><a href="https://raw.githubusercontent.com/wingmingchan64/Dufu-Analysis/refs/heads/main/%E8%B3%87%E6%96%99%E5%8C%AF%E7%B8%BD/3789.txt">《秋興八首》（Raw view）</a></li>

</ul>
-->
<!--
<li><a href=""></a></li>
<li><a href=""></a></li>
<li><a href=""></a></li>
<li><a href=""></a></li>
</ul>
-->