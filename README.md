# 杜甫全集、控制器、注本、引書來源

Status: Draft

---

## 如何「玩」杜甫詩？

讀了一輩子的杜詩，同時作爲一個電腦科學工程師，我一直在嘗試回答以下幾類問題：

- 杜詩正文：如何擁有一杜甫全集數碼文本，其中不含任何錯字（如「迴」誤作「回」）、拆字（如「𡿒」拆成「山」「孽」）、簡體字（如「云」「雲」不分，「后」「後」相混，「干」「乾」顚倒，「幺」「麼」合一）？
- 杜詩搜索：如何從杜甫的一句詩，或者只有零星、不相連的幾個字開始，有效地找到杜甫之全詩？
- 生成注本：如何在不儲存有固定格式、固定內容的個別注本文本之前提下，生成、顯示某注本的原書原貌
	- <a href="https://github.com/wingmingchan64/CanonicalTextTrees/blob/main/corpus/dufu/杜詩鏡詮/views/0097.html">《杜詩鏡詮》之《自京赴奉先縣詠懷五百字》 HTML</a>
- 眾多注本的顯示：如何於某杜詩下，幷列數個注本（如仇兆鰲的《杜詩詳註》、浦起龍《讀杜心解》、楊倫《杜詩鏡銓》、蕭滌非主編《杜甫全集校注》、謝思煒《杜甫集校注》）之注文、評論？
- 一對多：如何以同一組資料，生成數以千計的、內容各自不同的幷列注本、幷列版本、詩文與注文、評論的部分分列的文檔（如只有《北征》的頭十句及其注釋，或只有《北征》的詩文以及各家對《北征》的評論）？
- 眾多全集：如何生成杜甫全集帶各詩的白話文翻譯（或英譯、日譯）、杜甫全集帶王嗣奭《杜臆》的評論、杜甫全集帶平仄、韻部說明？
- 注本注文之分類、統計：如何不必把某書從頭到尾翻閱一遍，卽可回答「在趙次公注中，有多少條引用了《論語》」、「在仇兆鰲的《杜詩詳註》中，有多少條王嗣奭《杜臆》原書所缺的引文」、「蕭滌非主編《杜甫全集校注》全書（頭十一冊）共有多少條注文」一類之問題？
- 杜詩詞典之編纂：如何用程式自動編纂一本集諸注本注文之杜詩詞典？
- 如何在某杜詩注文之下，自動列出注文所引用之典籍（如《論語》、《史記》）之原文？
- 如何以同一套原始資料、各杜著述資料，以及相關之後設資料，同時回答以上所有問題？

---

## 關鍵的頭三步

要回答上述的各類問題，關鍵的第一步是把杜甫詩文與各家關於杜甫詩文的文字內容完全、徹底、乾淨地分隔開。

關鍵的第二步是采用樹結構來儲存各種資料，以達到任何文字內容均有層次結構、可快速作內容搜索、定位的操作。

關鍵的第三步是生成一棵專屬於某詩的資料樹，其內容視乎需要可多可少，少則只有一句詩，多則可包含該詩全文、十數個杜著述關於該詩的所有內容（異文、注釋、評論、備考、校記等）。

---

## 系統宣言

這裏推介的是一套以樹結構爲基礎的理論框架（a tree-based theoretical framework）：
- 適用於任何語言的文學資料（globally applicable to any literature）
- 展示如何儲存、組織資料（a way of storing and organizing data）
- 展示如何辨認、定位資料（way of identifying and locating data）
- 展示如何生成資料樹（creating data trees）
- 多種顯示同一資料的方式（multiple ways of presenting data）

The system is a theoretical framework for storing, organizing, identifying, locating, and presenting textual data. Although developed through the study of Du Fu and the vast body of related commentaries, its underlying principles are not limited to Chinese literature. The framework is designed to be applicable to any textual tradition. Texts are represented as trees, relationships are expressed through metadata, and different presentations are generated from the same underlying data structures.

---

## 三個關於杜甫詩文的儲存庫（Repositories）

- 模型（Model）： `DuFu`，杜甫全集（默認版本）、杜詩文基準正文樹
- 控制器（Controller）： `Dufu-Analysis`，PHP、Python 程式
- 模型（Model）、面貌（View）： `CanonicalTextTrees`，杜著述正文樹、JSON/JSONL、後設資料樹、以控制器生成的面貌文檔樣本、杜著述引用書籍（《論語》、《史記》等）正文樹

---

## 指導原則

- MVC 模式
- 只儲存原始資料、基於原始資料而生成之 JSON 資料庫，以及生成資料、生成面貌（views）之 PHP、 Python 程式 （controller），而不儲存面貌文檔本身（少量樣本除外）
- 模型（model）有三個主要部分：
  - 儲存杜詩文之基準正文樹（canonical text trees）
  - 儲存各種杜著述（注本、評本）原文之正文樹、引用典籍之正文樹
  - 儲存聯係前二者之後設資料指令樹
- 此三部分均爲樹結構
- 以基準正文樹、杜著述正文樹、後設資料指令樹，共同生成無所不包的資料樹
- 以一展示層（presentational layer）生成各種面貌（views）
- 還原某版本、某注本原來之模樣，如《全唐詩》之杜甫部分，屬於生成面貌（views）之層次
- Controller 亦生成 meta-metadata：後設資料標記之索引、分類、統計資料
- 杜甫詩文搜索采用樹路徑算法
- 基準正文樹路徑可體現爲坐標；坐標集乃一封閉系統，可盡數羅列
- 此模式只負責原始資料之有機分解（model）、按需要重新組合，由控制器（controller）負責；至於最後成品，卽面貌（views)之生成，則爲展示層（presentational layer）之責任

---

## 全是樹，爲甚麽？

- 杜甫詩文、杜著述/引用典籍內容、後設資料，三者均儲存於樹結構中
- 樹結構功能繁多（遞歸遍歷、截枝、嫁接、插入或替換文字內容，等等）
- 從樹根（root）開始的每條路徑都是獨特（unique）的，因此可以作爲任何節點的主鍵（primary key）
- 方便提取文字：利用樹路徑，可輕易提取所需文字
- 方便搜索：以樹路徑爲基礎，可生成各種索引，以便快速搜索
- 樹路徑與杜詩文文字可輕易互相轉換，人手編輯之後設資料指令可用文字（如《自京赴奉先縣詠懷五百字》中之「契闊」），系統內部自動轉換成 `0668,5,2,4-5`
- 顆粒度：不同樹種所儲存之文字內容之顆粒度，可按需要（還要考慮文件大小）而決定
  - 杜甫詩文以字爲最小單位，此爲提取、搜索之最小單位
  - 引用典籍，一般以句爲最小單位
  - 杜著述（注本、評本）一般以行、段爲最小單位
- 不同版本、資料來源之混合：樹型結構容許嫁接不同來源之子樹，以生成各種混合版本
- 後設資料樹之樹路徑爲程式指令
- 後設資料樹之樹路徑可用後設-後設資料修改、操作
- 後設資料單元（metadata component)亦輸出過渡性之樹型結構，成爲展示單元（presentational component）之輸入材料；過渡性樹型結構內存各種關於範圍、格式等資料
- 同一過渡性樹型結構，可按需要生成各種不同之最終面貌文本

---

## 基準正文樹

- 基準正文指規範化後之杜詩文默認版本的內容
- 儲存杜詩文之樹結構爲基準正文樹；例：<a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/schemas/json/base_text/0013-1.json">0013《題張氏隱居二首》其一</a>

基準正文樹之特點：

- 此樹乃一有層級性（hierarchical）之容器
- 樹中之終端節點（terminal nodes），卽樹中之任何一字，均可被刪除，亦可用任何不限字數、不限語言之文字替換
- 樹中可隨意添加儲存資料的錨（anchors）
- 以樹爲基礎，可生成路徑→文字（以路徑提取文字）、文字→路徑（以文字搜索路徑）之各種索引
- 以遞歸遍歷（recursive traversal）可以壓扁樹結構以提取文字、搜集樹中的資料

基準正文樹：爲甚麼

- 杜詩文默認版本只有一個來源
- 以路徑提取樹中文字
- 所有面貌（views）之生成，均用樹路徑提取文字，不另儲存拷貝之文字
- 樹路徑可用作索引、交叉參考之媒介
- 以一基準正文樹爲基礎，樹結構可以擴充爲資料樹

---

## 引用古籍正文樹、杜著述正文樹

- 杜著述指出現於是杜甫之後，討論杜甫或他的作品的任何文獻
- 引用古籍指在某杜著述中被引用的、成書於杜甫之前或與之同時的典籍，像《詩經》、《論語》、《史記》等
- 引用古籍正文樹爲儲存引用古籍內容的樹結構
- 杜著述正文樹爲儲存某杜著述不含基準正文的著述內容的樹結構

---

## 後設資料指令樹

後設資料指獨立於杜甫詩文、杜著述、引用典籍之外的、描述原始資料的第二級、甚至第三級的資料。第二級之後設資料負責聯係基準正文樹、杜著述正文樹/引用古籍正文樹。第三級後設資料（後設後設資料）可修改儲存第二級資料之後設資料指令樹，幷提供爲第二級後設資料之分類、統計而設立之機制。

後設資料指令樹爲具層級結構的指令集，每條樹路徑均爲一特定指令，負責聯係前述之三種正文樹。

後設資料指令樹路勁之三大用途：

- 路勁含杜著述、引用古籍之路徑（資料之來源），以及基準正文樹之錨（資料之去處）
- 路勁含格式（style）資料
- 杜著述內容之分類（異文、夾注、旁注、眉批、評論等）

此三樹設計之幾個優點：

- 杜甫詩文原文、注本之注文/引書原文二者完全分離
- 所有注本共用一套基準正文樹，不必重複詩文，卻能生成無數版本、格式
- 注文不帶基準正文，亦無號碼聯係，但能生成句注、行注、數碼注各種格式
- 一棵基準正文樹可同時與 M 棵杜著述、 N 棵引用典籍樹相聯係
- 後設資料樹除提供指令路徑外，亦提供後設後設資料

---

## 正文樹之坐標、路徑

<p>貫穿整個資料庫之搜索鍵乃一坐標系統。例：</p>
<ul>
<li>默認版本： <code>〚0003:〛</code>指《望嶽》</li>
<li>默認版本： <code>〚3789:2:〛</code>指《秋興八首》其二</li>
<li>默認版本： <code>〚3789:2:12-13〛</code>指《秋興八首》其二之首、頷二聯「夔府孤城落日斜，每依北斗望京華。聽猿實下三聲淚，奉使虛隨八月槎。」</li>
<li>默認版本： <code>〚0003:3.1.2〛</code>指《望嶽》中第三行第一句第二字「宗」</li>
<li>默認版本： <code>〚0003:3.1.2-4〛</code>指《望嶽》中第三行第一句第二至第四字「宗夫如」</li>
<li>注本：<code>〚郭0001:〛</code>指郭知達《新刊校定集注杜詩》之《奉贈韋左丞丈二十二韻》</li>
<li>注本子版本：<code>〚郭⸨聶⸩ 0001:〛</code>指《新刊校定集注杜詩》聶巧平點校本《奉贈韋左丞丈二十二韻》</li>
</ul>
<p>坐標有兩重功能，第一，它標明了某詩文片段之確切位置；第二；它顯示如何從樹根（詩碼）到達該詩文片段之路徑。</p>

<p>系統內部使用與坐標等値之樹路徑。例如，<code>〚0003:〛</code> 與 <code>0003</code> 等値，<code>〚3789:2:〛</code> 與 <code>3789,2</code> 等値，<code>〚0003:3.1.2-4〛</code> 與 <code>0003,3,1,2-4</code> 等値，等等。</p>

<p>與杜詩默認版本配套之坐標，共四十多萬個。（<a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/schemas/json/coords/%E9%BB%98%E8%AA%8D%E8%A9%A9%E6%96%87%E6%AA%94%E7%A2%BC_%E5%AE%8C%E6%95%B4%E5%9D%90%E6%A8%99%E8%A1%A8.json">默認詩文檔碼_完整坐標表</a>）

---

## 坐標、古注本所用之夾注、現代注本所用之數字碼之語義分別

不管是古注本所用之夾注，還是現代注本所用之數字碼，均有一個格式上之限制：除非重複杜詩原文，否則無法清楚顯示注文所屬。試考慮以下例子：

岱宗夫如何？齊魯青未了。<sub>[一]</sub>
	
[一]趙云：言其山之長大。東嶽謂之岱宗。《書》云：東巡狩，至於岱宗是也。

趙次公此注，注的是這兩句詩的哪個部分？「東嶽謂之岱宗。《書》云：東巡狩，至於岱宗是也。」注的是「岱宗」二字，而「言其山之長大。」則注「齊魯青未了」一句。卽使把文字改爲：

岱宗<sub>[一]</sub>夫如何？齊魯青未了。<sub>[二]</sub>
	
[一]趙云：東嶽謂之岱宗。《書》云：東巡狩，至於岱宗是也。
[二]趙云：言其山之長大。

仍然無法回答：注[二]注的是「齊魯青未了」、「青未了」、「未了」，還是「了」？

坐標標注的不只是某字（之後之位置），而是某字、某片段、某句、某行，甚至某幾行、組詩中的某首。「岱宗」之坐標是〚0003:3.1.1-2〛， 「齊魯青未了」之坐標是〚0003:3.2.1-5〛，「青未了」之坐標是〚0003:3.2.3-5〛，而「了」字之坐標是 〚0003:3.2.5〛。只要注文內容有清楚之界限，相應坐標就可以清楚地標明所屬。必要時，可用一坐標集，例如要列舉不相連的幾句詩文、甚至不屬同一首詩的詩文。要自動編纂杜詩詞典，此步絕不可少。

也只有利用坐標/路徑，注文之適用範圍方可毫不含糊地標明。

---

## 後設資料樹之路徑

有別於正文樹，後設資料樹幷不儲存文字資料。後設資料樹乃一儲存指令之樹型結構，從樹根開始，到某個終點節點爲止，其間的樹路徑乃一指令。例子：

>`JINGQUAN_0097_注釋_0668,5,2,4-5_JINGQUAN,0097,4_insert`

此路徑含六個部分：

- JINGQUAN：代表楊倫《杜詩鏡銓》
- 0097：《杜詩鏡銓》中《自京赴奉先縣詠懷五百字》之詩碼
- 注釋：此指令爲一注釋指令（默認指令爲 `insert`）
- 0668,5,2,4-5：基準正文樹路徑，指向「契闊」二字
- JINGQUAN,0097,4：《杜詩鏡銓》中《自京赴奉先縣詠懷五百字》之第四段文字「《詩注》：契闊，勤苦也。」
- insert：系統指令，把「《詩注》：契闊，勤苦也。」一段文字插入路徑爲 `0668,5,2,a` 之錨中

樹結構（tree structure) 有一個特點：樹中任何節點（node），連帶整棵以此節點爲根（root）之子樹，可以從樹中抽離，成爲獨立的樹。在後設資料樹中，注釋、評論等節點（詩碼之子節點）均可以獨立出來，成爲獨立的樹。這意味著用者可以只用一個或多個子節點，而非用全樹。如此，用者可以生成一個包含像仇兆鰲《杜詩詳註》之注釋、楊倫《杜詩鏡銓》之評論、蕭滌非《杜甫全集校注》之備考之混合版本之面貌。自由組合，乃是此系統之一大特色。

---

## 過渡性質之資料樹

在後設資料指令執行以後，基準正文樹成爲一過渡性質之資料樹：

<pre>
            "2": {
                "1": "白",
                "2": "首",
                "3": "甘",
                "4": "契〈夾注*0668,5,2,4*音挈。〉",
                "5": "闊",
                "p": "。",
                "a": "〈注釋*0668,5,2,4-5*《詩注》：契闊，勤苦也。〉"
            },
</pre>

負責生成面貌之展示單元（presentational component）可把 `〈注釋*0668,5,2,4-5*《詩注》：契闊，勤苦也。〉` 變成 `<span class="注釋">《詩注》：契闊，勤苦也。</span>`，而含範圍標記之路徑 `0668,5,2,4-5`（指向「契闊」之區間）亦可用於 style 或 JavaScript 中。

從手編基準正文到面貌生成的整個流程的說明，參看<a href="https://github.com/wingmingchan64/Dufu-Analysis/tree/main/docs/workflow">workflow</a>。

---

<h2>版本目錄（JSON）</h2>
<p>這裏亦提供重要注本頁碼之索引，包括注本之子版本之實體書、電子書頁碼、下載鏈接等。</p>
<ul>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E3%80%8A%E5%85%A8%E5%94%90%E8%A9%A9%E3%80%8B/catalog/%E5%85%A8%E7%9B%AE%E9%8C%84.json">《全唐詩》杜甫部分</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E6%9E%97%E7%B9%BC%E4%B8%AD%E8%BC%AF%E6%A0%A1%E3%80%8A%E6%9D%9C%E8%A9%A9%E8%B6%99%E6%AC%A1%E5%85%AC%E5%85%88%E5%BE%8C%E8%A7%A3%E8%BC%AF%E6%A0%A1%E3%80%8B/catalog/%E8%B6%99%E7%9B%AE%E9%8C%84.json">林繼中輯校《杜詩趙次公先後解輯校》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E9%83%AD%E7%9F%A5%E9%81%94%E3%80%8A%E6%96%B0%E5%88%8A%E6%A0%A1%E5%AE%9A%E9%9B%86%E6%B3%A8%E6%9D%9C%E8%A9%A9%E3%80%8B/catalog/%E9%83%AD%E7%9B%AE%E9%8C%84.json">郭知達《新刊校定集注杜詩》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E7%8E%8B%E5%97%A3%E5%A5%AD%E3%80%8A%E6%9D%9C%E8%87%86%E3%80%8B/catalog/%E5%A5%AD%E7%9B%AE%E9%8C%84.json">王嗣奭《杜臆》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E4%BB%87%E5%85%86%E9%B0%B2%E3%80%8A%E6%9D%9C%E8%A9%A9%E8%A9%B3%E8%A8%BB%E3%80%8B/catalog/%E4%BB%87%E7%9B%AE%E9%8C%84.json">仇兆鰲《杜詩詳註》</a></li>

<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E8%95%AD%E6%BB%8C%E9%9D%9E%E4%B8%BB%E7%B7%A8%E3%80%8A%E6%9D%9C%E7%94%AB%E5%85%A8%E9%9B%86%E6%A0%A1%E6%B3%A8%E3%80%8B/%E8%95%AD%E7%9B%AE%E9%8C%84.json">蕭滌非主編《杜甫全集校注》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E8%AC%9D%E6%80%9D%E7%85%92%E3%80%8A%E6%9D%9C%E7%94%AB%E9%9B%86%E6%A0%A1%E6%B3%A8%E3%80%8B/catalog/%E8%AC%9D%E7%9B%AE%E9%8C%84.json">謝思煒《杜甫集校注》
</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E4%B8%8B%E5%AE%9A%E9%9B%85%E5%BC%98%E3%80%81%E6%9D%BE%E5%8E%9F_%E6%9C%97%E3%80%8A%E6%9D%9C%E7%94%AB%E5%85%A8%E8%A9%A9%E8%A8%B3%E6%B3%A8%E3%80%8B/catalog/%E8%A8%B3%E7%9B%AE%E9%8C%84.json">下定雅弘、松原_朗《杜甫全詩訳注》</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E7%89%88%E6%9C%AC%E7%9B%AE%E9%8C%84%E5%B0%8D%E7%85%A7%E8%A1%A8.json">版本目錄對照表</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E9%BB%98%E8%A9%A9%E7%A2%BC_%E7%89%88%E6%9C%AC%E8%A9%A9%E7%A2%BC%E5%B0%8D%E7%85%A7%E8%A1%A8.json">默詩碼_版本詩碼對照表</a></li>
<li><a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E3%80%8A%E5%85%A8%E5%94%90%E8%A9%A9%E3%80%8B/versions/%E5%85%A8%E7%89%88%E6%9C%AC%E8%B3%87%E6%96%99.json">《全唐詩》之版本資料</a></li>
- 整理中：錢謙益《錢注杜詩》目錄、楊倫《杜詩鏡銓》目錄
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
<p>基準正文樹、評注原始資料+後設資料標記可支持某杜注本之還原，卽此注本原書之生成。此模式最大之優點：同一基準正文樹，結合不同注本、版本之原始資料、後設資料，可生成無數之注本、版本，亦可同時展示、幷列不同注本、版本之資料。限於版權問題，只提供不受版權保護之原始資料及其後設資料。受保護之注本，如蕭滌非主編《杜甫全集校注》，則單提供後設資料。</p>
<p>注本還原亦爲面貌（view）層次之產物。以下是幾個例子（例子均以程式生成）：</p>

- <a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E3%80%8A%E5%85%A8%E5%94%90%E8%A9%A9%E3%80%8B/samples/0002.md">《全唐詩·送高三十五書記》</a>
- <a href="https://github.com/wingmingchan64/Dufu-Analysis/blob/main/packages/%E9%83%AD%E7%9F%A5%E9%81%94%E3%80%8A%E6%96%B0%E5%88%8A%E6%A0%A1%E5%AE%9A%E9%9B%86%E6%B3%A8%E6%9D%9C%E8%A9%A9%E3%80%8B/samples/0001.md">郭知達《新刊校定集注杜詩·奉贈韋左丞丈二十二韻》</a>

<h2>面貌之多元</h2>
<p>基準正文樹、評注原始資料+後設資料標記之二元分離，可支持同一版本（如仇兆鰲之《杜詩詳註》）之五個不同面貌：</p>
<ul>
<li>以聯注（行注）形式爲主，注文插入詩文中間，卽傳統古書之面貌</li>
<li>以聯注（行注）形式爲主，注文置於詩文之後，以號碼爲聯係，如現代排版之《杜詩詳註》</li>
<li>以字注、詞注形式爲主，注文插入詩文中間，如傳統古書之讀音、異文夾注</li>
<li>以字注、詞注形式爲主，注文置於詩文之後，以號碼爲聯係，如今人之注本</li>
<li>我設計之形式，一行（或一聯）之詩文，後接該行（聯）之各種大小注文；此面貌適用於羅列不同注者之注文，評論則可散於其中，亦可置於詩文之後</li>
</ul>
<p>由於這種二元分離性，一棵《北征》之基準正文樹，配合恰當、配套之原始資料，加上對應之後設資料，可生成《北征》之英譯、日譯，甚至可以生成李白之《將進酒》，或 Harry Potter 七書中之某段文字。</p>


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