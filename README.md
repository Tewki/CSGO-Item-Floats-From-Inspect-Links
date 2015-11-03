### The knowledge you'll need:
How write in a programming language.

How to copy paste and maybe write a bit of your own code.

How do think.
    
	
### To start off
Learn what protobuf is.

Google SteamKit

Learn a programming language? Maybe... Omg you should totally start with C++ (Or CSS/HTML)... Said anyone who hasn't learned 
how to code yet...

### What you resources you'll need
The protobufs, [SteamKit helps you](https://github.com/SteamRE/SteamKit/blob/f94c56ce371b2ec76794ed284b80582bae47cea4/Resources/Protobufs/csgo/cstrike15_gcmessages.proto#L657-L701 "Oh shit I just gave u the whole thing...").

A simple bot that uses it, [Here you go](https://github.com/joshuaferrara/node-csgo "Do note it will not be pleasant.").

_Knowledge, 2.000 books and a lamborghini._

### Making the request
```
  message CMsgGCCStrike15_v2_Client2GCEconPreviewDataBlockRequest {
      optional uint64 param_s = 1; <-  SteamID
      optional uint64 param_a = 2; <-  AssetID
      optional uint64 param_d = 3; <-   DickID
      optional uint64 param_m = 4; <- MarketID
  }
```

Sample Link's
```
+csgo_econ_action_preview S76561198105687636 A1819544291 D12163248981785403065
+csgo_econ_action_preview M76561198105687636 A1819544291 D12163248981785403065
```

See the connection? 
Good.

So what should you send?

```
{
	param_s: "76561198105687636",
    param_a: "1819544291",
    param_d: "12163248981785403065"
}
```

Notice the string usage, JS loves fucking around with big ints.

##### Now how do we send it? 

Look in the source and figure it out but here's a tip

[Sample](https://github.com/joshuaferrara/node-csgo/blob/74c577cf2d9d958f0263d2f849a08fc80052a00d/handlers/match.js#L60-L78) to go from.


Take the content above, change the 
```CMsgGCCStrike15_v2_MatchListRequestLiveGameForUser``` to ```CMsgGCCStrike15_v2_Client2GCEconPreviewDataBlockRequest```

And ```k_EMsgGCCStrike15_v2_MatchListRequestLiveGameForUser```
To ```k_EMsgGCCStrike15_v2_Client2GCEconPreviewDataBlockRequest```

##### But pappa cawky, what about responds?

Again look in the source, [for lazy people](https://github.com/joshuaferrara/node-csgo/blob/74c577cf2d9d958f0263d2f849a08fc80052a00d/handlers/match.js#L202-L209).

The thing you need for this is just [this msg](https://github.com/SteamRE/SteamKit/blob/f94c56ce371b2ec76794ed284b80582bae47cea4/Resources/Protobufs/csgo/cstrike15_gcmessages.proto#L699) & [the ID](https://github.com/SteamRE/SteamKit/blob/f94c56ce371b2ec76794ed284b80582bae47cea4/Resources/Protobufs/csgo/cstrike15_gcmessages.proto#L61)

##### Ok, I learned how to do those steps now what about the float, there's no fucking float in here you fucking scamming piece of fucking shit (Actual message from a "dev", really cute)

It's called [paintwear](https://github.com/SteamRE/SteamKit/blob/f94c56ce371b2ec76794ed284b80582bae47cea4/Resources/Protobufs/csgo/cstrike15_gcmessages.proto#L672), and it's in UInt32 cuz fuck floats.

Now to just spoonfeed you so you don't have to spend like 4 hours looking at how to make it into a float,

```
var lazyFunctionWithIncorrectStuffButWhyNot(annoyingFuckingUnsignedShit) {
	buf = new Buffer(4);
    buf.writeUInt32LE(+annoyingFuckingUnsignedShit, 0);
    return buf.readFloatLE(0).toString()
}
```

##### What about origin?

http://tf2tools.net/articles/singleorigin

##### So lets recap

```
message CEconItemPreviewDataBlock {
	optional uint64 itemid = 2; <- Asset ID
	optional uint32 defindex = 3; <- Gun type iirc
	optional uint32 paintindex = 4; <- Skin index ID (Like 415-421 is the ids for the dopplers)
	optional uint32 paintwear = 7; <- Float value
}
```


### On another note
For anything, calling stuff malware is just pathetic tbh when the other sites (csgo.exchange, csgozone, csgofloat) is trying to make bucks out of simple stuff that requires almost no hardware (Bot does not run the game), no skill, no knowledge (minus some parts) or anything.

Specially when the site you're calling malware & untrustworthy has no login, is not asking for anything and is fully free and well ad-free, and is actually not even logging stuff as I like lowendstuff and access log is just wasteful; plus I don't rly care since it was just to kill the market for sites selling it, like the pathetic attempt by csgo.exchange.

While we're at csgo.exchange, it requires almost nothing to run it smoothly so good job at paying for nothing; bit of optimization and less retarded shit and there you go, budget cutted & site is faster.

Also didn't give a pure source cuz then you would just run it and learn nothing, if you know a language you can at least get better at it and like start testing stuff out.

Plus in real I'd rather see this fixed as why do we need to see the actual full value of the float, why not a rounded value since all that matters is that it looks the same which you don't need the actual value for unless u wanna count pixels.

### Contact

* http://steamcommunity.com/id/CAWKCAWKCAWKCAWK
* admin@neku.jp
