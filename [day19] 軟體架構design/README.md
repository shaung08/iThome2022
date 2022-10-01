# [day19] 軟體架構design
### design pattern
在軟體工程中，設計模式（design pattern）是對軟體設計中普遍存在（反覆出現）的各種問題，所提出的解決方案，目前軟體將design pattern在分成下面三項。
* Architecture Patterns：解決軟體系統架構層面的問題。如：MVC (Model-View-Controller pattern) 架構，Layer等等
* Design Patterns：提供了改善軟體系統中子系統與元件 (components)的方案。軟工中常見的模式如：Observer，Facade，Adapter等等
* Idioms：是一種 lowest-level patterns，為 Programming (程式撰寫)層級提供程式改善方案，主要透過程式語言的解決方案來實現。

下列網站介紹有關軟體程式撰寫相關design，內容相當精采有興趣可以閱讀一遍。
(https://github.com/kamranahmedse/design-patterns-for-humans#creational-design-patterns)[https://github.com/kamranahmedse/design-patterns-for-humans#creational-design-patterns]

### Test-Driven Development
TDD：Test-driven development測試驅動開發。是一種開發流程，觀念是「先寫測試，在進入開發工作」。在進行開發工作以前，編寫測試，先模擬欲測試的情境，日後在進行維護時方便修改測試並可以迅速deployment。

## 參考 
* https://www.guru99.com/test-driven-development.html
* https://ithelp.ithome.com.tw/articles/10234830
* https://github.com/kamranahmedse/design-patterns-for-humans#creational-design-patterns
* https://medium.com/fcamels-notes/test-driven-development-%E8%A7%A3%E6%B1%BA%E4%BA%86%E4%BB%80%E9%BA%BC%E5%95%8F%E9%A1%8C-%E6%88%96%E6%98%AF%E8%A3%BD%E9%80%A0%E6%9B%B4%E5%A4%9A%E5%95%8F%E9%A1%8C-937db879f695
* https://medium.com/%E6%88%91%E6%83%B3%E8%A6%81%E8%AE%8A%E5%BC%B7/tdd-test-driven-development-%E6%B8%AC%E8%A9%A6%E9%A9%85%E5%8B%95%E9%96%8B%E7%99%BC-%E5%85%A5%E9%96%80%E7%AF%87-e3f6f15c6651