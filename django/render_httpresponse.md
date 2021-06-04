## Rendering(in web)
랜더링이란 웹사이트 코드를 사용자가 웹을 방문했을때 보는 인터렉티브한 페이지로 **변환하는 과정**을 말한다.

## HttpResponse
- `HttpResponse()`는 템플릿으로 context를 전달한다. 
- 랜더링하지 않고 그냥 HttpResponse로만 리턴하게 되면 html, css, js등이 제대로 나오지 않고 Response로 보내준 데이터만 출력된다.
- 그러므로 장고 튜토리얼에 있는 예시처럼 페이지를 제대로 출력하기 위해서는 `loader`를 임포트하여 랜더링을 해주어야 한다.
```python
def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))
```

## Render
- `render()`는 위의 과정(context 전송 + 랜더링)을 한번에 할 수 있다.
  - *context: context는 템플릿에서 쓰이는 변수명과 Python 객체를 연결하는 사전형 값
```python
def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
```

<details>
  <summary>여담</summary>
  
레거시에 `HttpResponse()`와 `render()`가 혼용되고 있는데 비슷한 일을 하고 있는 것 같으면서도 뭐가 다른건지 헷갈렸다. 단순히 api를 호출하여 response로 받는 데이터만 사용되는 경우라면 `HttpResponse()`를 
  쓰고 랜더링까지 필요한 경우라면 `render()`를 쓰면 되겠다.
</details>

### Reference
- https://docs.djangoproject.com/ko/3.2/intro/tutorial03/
