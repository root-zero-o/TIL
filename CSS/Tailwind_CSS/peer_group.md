# Group & Peer modifier

## Group modifier
- 부모 요소의 상태에 따라 스타일을 바꾸고 싶을 때 사용한다.
- className : ```group-*``` 형태로 준다.(예 : ```group-hover```)
```javascript
<a href="#" class="group block max-w-xs mx-auto rounded-lg p-6 bg-white ring-1 ring-slate-900/5 shadow-lg space-y-3 hover:bg-sky-500 hover:ring-sky-500">
                  // 1. 부모요소에 group이라는 class를 준다. 
  <div class="flex items-center space-x-3">
    <svg class="h-6 w-6 stroke-sky-500 group-hover:stroke-white" fill="none" viewBox="0 0 24 24"><!-- ... --></svg>
                                        // 2. group class를 받은 부모요소가 hover되면 나타나는 변화를 써줌
    <h3 class="text-slate-900 group-hover:text-white text-sm font-semibold">New project</h3>
  </div>
  <p class="text-slate-500 group-hover:text-white text-sm">Create a new project from a variety of starting templates.</p>
</a>
```

## Peer modifier
- sibling 요소의 상태에 따라 스타일을 바꾸고 싶을 때 사용한다.
- className : ```peer-*``` 형태로 준다. (예 : ```peer-invalid```)
```javascript
<form className="flex flex-col space-y-2 p-5">
        <input 
          type="text" 
          required
          placeholder='Username' 
          className='border p-1 peer border-gray-400 rounded' 
                              // 1. sibling 요소에 peer라는 class를 준다
        />
        <span className="hidden peer-invalid:block peer-invalid:text-red-500">This input is invalid</span>
                                // 2. peer class를 받은 sibling 요소가 invalid 상태이면 나타나는 변화를 써줌
        <span className="hidden peer-valid:block peer-valid:text-teal-500">Awesome userName</span>
                                // 3. 서로 다른 상태일 때의 변화를 써줄 수도 있다.
        <input type="submit" value="Login" required className='bg-white'/>
      </form>
```
