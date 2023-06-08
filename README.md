# 如何建立 prebid docker 環境

1. clone prebid
```
git clone https://github.com/prebid/Prebid.js.git
```

2. 建立image
```
docker build -t mctw_prebid:latest .
```


3. run container
 ```
docker run -it \
--name mctw_prebid \
-p 9002:9002 \
-d mctw_prebid:latest start
 ```

4. create Google Ad Manager order
   範例使用的是 teads 為合作對象
   dry-run 不會正式建立訂單，僅驗證yaml
```
line_item_manager create 你的yaml路徑 \
--dry-run \
--private-key-file 'gcp api 憑證' \
--network-code 聯播網代碼 \
--network-name '聯播網顯示名稱' \
--bidder-code '你合作的 Bidder Adapters'
```

會建立一筆訂單，兩筆測試委刊項
```
line_item_manager create 你的yaml路徑 \
--test-run \
--private-key-file 'gcp api 憑證' \
--network-code 聯播網代碼 \
--network-name '聯播網顯示名稱' \
--bidder-code '你合作的 Bidder Adapters'
```
建立正式訂單
```
line_item_manager create 你的yaml路徑 \
--private-key-file 'gcp api 憑證' \
--network-code 聯播網代碼 \
--network-name '聯播網顯示名稱' \
--bidder-code '你合作的 Bidder Adapters'
```



5. CustomTargetingError.VALUE_STATUS_NOT_ACTIVE
   注意的是如果你設定了美金為價格區間，在健值這部分要注意的是，Ad Manager必須設定到小數點第二位
   例如 1塊錢 須設置為 1.00，不可只設定為1 or 1.0
