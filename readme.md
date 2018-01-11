# Azure 使用心得

以下主要根據之前使用 AWS 及 SoftLayer 的經驗 (少部分在 Google Cloud Platform 上，TPU 登記但尚未有機會測試)，簡要就 Deep Learning 實作上的特殊性，在技術平台及商業模式兩個面向，對 Azure 未來發展提供幾點個人意見 (各家雲端平台上因功能繁多且發展快速，如有失準還請包涵):

* GPU 

  * 對 SoftLayer 印象最深的是 Bare Metal 的效能及線上客服的效率，經驗上遠勝 AWS，因為 GPU 在雲端的計價相對地高，因此，如何協助開發人員節費，應該是值得深入著墨的部分，例如，GPU及VM的開啟及關閉，應該有機會深入與 model training/testing 的執行整合，比如說 Keras 只取 best model 且 patience 次數已達、程式已決定不再往下執行時，應該要有簡便的方式停下雲端資源節費。Azure 在 "系統平台" 層次有許多 API 可管理雲端資源，但對開發人員來說，如果能在 Keras 層次一併處理，會更為直覺。 (tight coupling / loose coupling 各有優缺就是)

  * elastic 部分，同樣地，如果能夠深入依據 training 過程中 (如 TensorBoard log) 動態調整 GPU 資源，例如 loss 的曲線已經收斂不會再低了、GPU 就不要再下重本，類似這樣的功能對雲端業者及開發人員會是雙贏，因為開發人員知道雲端業者也想幫忙避免虛耗。

* 管理平台

  * 初步測試 Machine Learning Workbench 及 Machine Learning Experimentation 的印象是有幫助，但計費方式可能會影響開發人員使用意願，這部分的費用相較於 GPU 而言應該是小錢，建議對中小規模直接免費比較乾脆，獲利放在未來 GPU 用量比較實在。

  * 延續上面與 source code 深入整合的概念，Machine Learning Workbench 及 Experimentation 之類的管理功能，應該有機會無縫與 source code 或產出的 data 整合，例如 TensorBoard 方便看 log 一般，或又例如採取 grid search 探索最佳 model ，應該可以做到以程式依預設範圍自動化展開 grid search，並將過程中點點滴滴紀錄到 Azure ML 平台上，免除 model 設定及管理實驗結果的繁瑣人力。

以上幾點淺見。

Jason