# [day21] 軟體設計原則
### SOLID 原則
* Single-responsiblity principle
一個class內應該只有一個改變的理由，指是一個class應該只需要專注做一件事情。
* Open-closed principle
當你新增功能的時候，需能在不更改原本程式碼的情況下進行擴增，如此一來，可以增加維護性，降低原有的功能發生錯誤的機率，重用性的機率也會隨之提高。
* Liskov substitution principle
若是使用繼承，子類別實作的行為必須要與父類別或是介面所定義的行為一致，並且子類別要能夠完全取代掉父類別，若子類別沒有遵守LSP的情況下，使用者呼叫某個功能時可能會出現與預期的功能不相符合的問題。
* Interface segregation principle
在設計介面時，不應該放入不相關的method，例如在一個叫animal的abstract class內含有run()和fly()的method，由狗和鳥繼承，但是狗會跑卻不會飛，必須減少不當的設計。
* Dependency Inversion Principle
高階模組不要依賴低階模組，假設我有多個廠牌亮度不相同的燈泡，但是只要符合燈座的規格，都可以安裝上去，以這個範例來說，燈座的規格就是抽象模組。

### YAGNI 原則
對於專案實務上來說，這些預設立場的功能並沒有辦法在專案上實際運用，很有可能自己猜想覺得完美無缺，但實際真的運用時會有沒想到的例外處理。即便是寫了單元測試（Unit testing）去細心維護這些擴充的功能，在將來也很有可能因為文件規格的改動使得這些擴充的功能並不符合預期效益。

### DRY (Don't repeat yourself)
DRY (Don’t repeat yourself)，是敏捷開發的核心設計原則之一。DRY 原則規定，對於每個知識點，系統中都只有一個明確而權威的表示。這個原則倡導單一事實來源(single source of truth) 的哲學，適用於所有的軟體開發工作，包含文件、設計、測試。但此原則常常被誤解，不少人認為只要兩個程式片段長得一樣就是違反了 DRY 原則。事實上，有些情況中的重複並不是一件壞事，甚至有些沒有重複的程式卻違反 DRY 原則。本文將探討 DRY 原則的運用情境。

## 參考
* https://www.baeldung.com/solid-principles
* https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design
* https://deviq.com/principles/keep-it-simple
* https://www.interaction-design.org/literature/topics/keep-it-simple-stupid
* https://martinfowler.com/bliki/Yagni.html
* https://deviq.com/principles/yagni
* https://dzone.com/articles/software-design-principles-dry-and-kiss
* https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1001745#s5