nohup go run main.go > out.log 2>&1 &


nohup go run cmd/save/aggTradeMulti/bn/main.go > aggTrade.log 2>&1 &
tail -f aggTrade.log 

nohup go run cmd/save/allDepthMulti/bn/main.go > allDepth.log 2>&1 &
tail -f allDepth.log

nohup go run cmd/save/bookTickerMulti/bn/main.go > bookTick.log 2>&1 &
tail -f bookTick.log

nohup go  run cmd/save/linuxServer/main.go > linuxServer.log 2>&1 &