# Flex grow & shrink 조절하기 😎

## flex-initial
- 안에 있는 flex item이 수축되지만, 늘어나지는 않는다.

![화면 캡처 2022-07-26 194720](https://user-images.githubusercontent.com/97326130/180988712-49cb928b-2d38-4ddd-b619-f51159753b42.png)

```javascript
<div className="w-40 border-4 flex">  // 박스의 총 길이보다 짧으면 줄어든다.
   <div className="w-20 h-20 bg-rose-400 flex-initial">1번</div>
   <div className="w-20 h-20 bg-teal-400 flex-initial">2번</div>
   <div className="w-20 h-20 bg-blue-400 flex-initial">3번</div>
</div>
```

![화면 캡처 2022-07-26 194733](https://user-images.githubusercontent.com/97326130/180988862-beb6d454-a8ef-4212-857c-2d7e3c30053d.png)

```javascript
<div className="w-80 border-4 flex">  // 박스의 총 길이보다 길어도 늘어나지 않는다.
   <div className="w-20 h-20 bg-rose-400 flex-initial">1번</div>
   <div className="w-20 h-20 bg-teal-400 flex-initial">2번</div>
   <div className="w-20 h-20 bg-blue-400 flex-initial">3번</div>
</div>
```

## flex-1, flex-auto
- 늘어나고, 수축한다.
- 차이점
    - flex-1 :  ignoring its initial size
    - flex-auto : taking into account its initial size

![화면 캡처 2022-07-26 194720](https://user-images.githubusercontent.com/97326130/180989706-b8acd6f8-938d-41f5-9210-7879eebe8a90.png)

```javascript
<div className="w-40 border-4 flex">  // 박스의 총 길이보다 짧으면 수축한다.
   <div className="w-20 h-20 bg-rose-400 flex-1">1번</div>
   <div className="w-20 h-20 bg-teal-400 flex-1">2번</div>
   <div className="w-20 h-20 bg-blue-400 flex-1">3번</div>
</div>
```

![화면 캡처 2022-07-26 195318](https://user-images.githubusercontent.com/97326130/180989899-b942fec6-66e1-4421-8898-29a315f764ec.png)

```javascript
<div className="w-80 border-4 flex">  // 박스의 총 길이보다 길면 늘어난다.
   <div className="w-20 h-20 bg-rose-400 flex-1">1번</div>
   <div className="w-20 h-20 bg-teal-400 flex-1">2번</div>
   <div className="w-20 h-20 bg-blue-400 flex-1">3번</div>
</div>
```

## flex-none
- flex item이 늘어나지도, 줄어들지도 않는다.

![화면 캡처 2022-07-26 200303](https://user-images.githubusercontent.com/97326130/180991348-199b87d5-d029-425c-a21e-a32208b2b7e0.png)

```javascript
<div className="w-20 border-4 flex">  // 박스의 총 길이보다 짧아도 줄어들지 않는다.
   <div className="w-20 h-20 bg-rose-400 flex-none">1번</div>
   <div className="w-20 h-20 bg-teal-400 flex-none">2번</div>
   <div className="w-20 h-20 bg-blue-400 flex-none">3번</div>
</div>
```

![화면 캡처 2022-07-26 194733](https://user-images.githubusercontent.com/97326130/180991513-994d7b19-2024-4bb4-bef0-d9ad97827290.png)

```javascript
<div className="w-80 border-4 flex">  // 박스의 총 길이보다 길어도 늘어나지 않는다.
   <div className="w-20 h-20 bg-rose-400 flex-none">1번</div>
   <div className="w-20 h-20 bg-teal-400 flex-none">2번</div>
   <div className="w-20 h-20 bg-blue-400 flex-none">3번</div>
</div>
```

## 참고
- https://tailwindcss.com/docs/flex
- 노마드코더 "캐럿마켓 클론코딩"
