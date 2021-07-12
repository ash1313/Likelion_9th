# BootStrap

### BootStrap

CSS/JavaScript 기반 웹 프레임워크(웹을 만드는 재료들의 모음)

+ 장점

  1. 공짜!

  2. 반응형 웹 지원(자동화면조정)

  3. 브라우저 호환성

     

+ 단점

  1. 딱 보면 티 남

  2. 성능이 다소 떨어짐

     

+  부트스트랩 CDN

  <head>태그 안에 넣기

+ jQuery CDN

  <head>태그 안에 넣기

+ 콘테이너

  `````HTML
  <div class="container">
      
  </div>
  `````

+ 버튼

  `````HTML
  <input type="submit" class="btn btn-primary">
  `````

+ 폼

  `````HTML
  <form action="전송받을대상">
          아이디 : <input type="text" name="id">
          비밀번호 : <input type="password" name="pw">
          <div class="form-group">
            <label for="exampleInputEmail1">이메일 주소</label>
            <input type="email" class="form-control" id="exampleInputEmail1" placeholder="이메일을 입력하세요">
          </div>
          <div class="form-group">
            <label for="exampleInputPassword1">암호</label>
            <input type="password" class="form-control" id="exampleInputPassword1" placeholder="암호">
          </div>
          <div class="form-group">
            <label for="exampleInputFile">파일 업로드</label>
            <input type="file" id="exampleInputFile">
            <p class="help-block">여기에 블록레벨 도움말 예제</p>
          </div>
          <div class="checkbox">
            <label>
              <input type="checkbox"> 입력을 기억합니다
            </label>
          </div>
          <button type="submit" class="btn btn-primary">제출</button>
  </form>
  `````

+ nav(탭형)

  `````HTML
  <ul class="nav nav-tabs">
    <li role="presentation" class="active"><a href="#">Home</a></li>
    <li role="presentation"><a href="#">Profile</a></li>
    <li role="presentation"><a href="#">Messages</a></li>
  </ul>
  `````

+ 진행바

  `````HTML
  80% Complete (danger)
  Copy
  <div class="progress">
    <div class="progress-bar progress-bar-success" role="progressbar" aria-valuenow="40" aria-valuemin="0" aria-valuemax="100" style="width: 40%">
      <span class="sr-only">40% Complete (success)</span>
    </div>
  </div>
  <div class="progress">
    <div class="progress-bar progress-bar-info" role="progressbar" aria-valuenow="20" aria-valuemin="0" aria-valuemax="100" style="width: 20%">
      <span class="sr-only">20% Complete</span>
    </div>
  </div>
  <div class="progress">
    <div class="progress-bar progress-bar-warning" role="progressbar" aria-valuenow="60" aria-valuemin="0" aria-valuemax="100" style="width: 60%">
      <span class="sr-only">60% Complete (warning)</span>
    </div>
  </div>
  <div class="progress">
    <div class="progress-bar progress-bar-danger" role="progressbar" aria-valuenow="80" aria-valuemin="0" aria-valuemax="100" style="width: 80%">
      <span class="sr-only">80% Complete (danger)</span>
    </div>
  </div>
  `````

  