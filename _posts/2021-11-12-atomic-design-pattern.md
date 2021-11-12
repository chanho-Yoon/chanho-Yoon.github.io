---
title: 'React와 Atomic'
excerpt: 'React에 atomic 디자인 패턴을 어떻게 적용했는지 포스팅 하겠습니다.' 
categories: [atomic]
tags: [atomic]
last_modified_at: 2021-11-12T01:18:00-19:00, 
toc: true 
toc_label: '목차'
sitemap :
changefreq : daily
priority : 1.0
---

# React와 Atomic 디자인 패턴 with Tailwind.CSS

> 이전 회사에서 React와 Atomic 디자인 패턴을 어떤식으로 적용하여 개발을 했었는지에 대해 이야기 할려고 합니다. 무조건적인 답이 아닌 이런식으로 아토믹 디자인 패턴을 적용했구나라고 봐주시면 감사하겠습니다. 
> 더불어 개발하면서 느꼈던 장점과 단점도 알아보겠습니다.

## Atomic이 뭔데?

![image](https://user-images.githubusercontent.com/54402926/141319350-c7df1d14-2215-446e-845d-aca7019a28ee.png)

작은 단위부터 만들고 그것들을 붙여 나가면서 하나의 page를 만들어가는 디자인 패턴입니다.

## Atomic 요소

> 아토믹 요소를 나누는 기준은 애매모호한게 정말 많습니다. 어디까지가 분자고 어디까지가 유기체로 봐야할지 경계를 구분하기가 되게 어려웠습니다. 지금 나누는 기준은 개발을 하면서 팀원과 상의하여 정한 기준입니다.<br /> 

### atoms (원자)
- 가장 작은 단위로 `Form`, `Box`, `Button`, `Ul`, `Li`, `Icon`, `Input`, `Span` 과 같이 하나의 요소를 말합니다.
- 원자는 최대한 다양한 state를 가지고 있도록 했습니다. 예를 들어 Box의 컬러가 여러개인데 각각 블루 박스, 레드 박스를 만들면 그만큼 작성해야할 원자도 많아지고 재사용성과 거리가 멀어진다고 판단했습니다. `<Box colorType="red"></Box>`이와 같이 작성하여 하나의 원자로 다양한 state값을 가질 수 있도록 작성했습니다. 

```tsx
  const Box = React.forwardRef<HTMLDivElement, BoxProps>(
  (
    {
      bgColorType,
      fontColor = 'white',
      allSizeType = 'small',
      fontSize,
      paddingSize,
      isRounded = true,
      fontWeightType = 'normal',
      className,
      ...props
    },
    ref
  ) => {
    return (
      <div
        className={`
            inline-block
            bg-${bgColorType}
            p-${paddingSize ? paddingSize : getPaddingSize(allSizeType)}
            text-${fontColor}
            text-${fontSize ? fontSize : getFontSize(allSizeType)}
            font-${fontWeightType}
            ${className}
            ${isRounded && 'rounded-m'}
          `}
        ref={ref}
        {...props}
      ></div>
    );
  }
);
```

- 자주 사용하는 div도 Flex라는 `atoms`로 만들어 아래와 같이 `props`로 전달 받아서 사용했습니다. 최대한 필수적이다 생각되는 props를 정했고 props에 없는 스타일링 요소가 필요할 경우는 `className`에 tailwind 스타일링 props를 전달하여 해결했습니다.
  
```tsx
const Flex = React.forwardRef<HTMLDivElement, FlexProps>(
  (
    {
      displayType = 'flex',
      flexDirection = 'row',
      alignItems = 'center',
      justifyContent = 'center',
      width = 'auto',
      height = 'auto',
      bgColorType,
      paddingSize,
      marginSize,
      gapSize,
      className,
      cursorType,
      ...props
    },
    ref
  ) => {
    return (
      <div
        className={`
          ${displayType}
          flex-${flexDirection}
          justify-${justifyContent}
          items-${alignItems}
          w-${width}
          h-${height}
          bg-${bgColorType}
          gap-${gapSize}
          p-${paddingSize && paddingSize}
          m-${marginSize && marginSize}
          cursor-${cursorType && cursorType}
          ${className}
        `}
        ref={ref}
        {...props}
      ></div>
    );
  }
); 

// 스타일링 props가 없을 땐 className props에 tailwind 스타일링 요소 추가
<Flex width={'full'} justifyContent={'end'} className={'relative'}></Flex>

```
### molecules (분자)

> 최소 2개, 최대 3개까지의 `atoms(원자)`를 기준으로 정했습니다. <br />또한 분자는 독립적으로 동작이 되어야한다는 것을 기준으로 정했습니다.

- atoms로 만들어진 것을 이용해 합한 그룹으로 HashTag Box가 있다고 가정할 때 `Box` + `Span` 과 같이 조합하여 만들어집니다.
- ```html
  <Box>
    <Span></Span>
  </Box>
  ```

### organisms (유기체)

> 원자와 분자를 합쳐 유기체를 작성합니다. 이때 분자와 분자만을 합쳐 유기체만을 만드는게 아닌 원자도 같이 활용하여 유기체를 만들어나갔습니다.

- molecules로 만들어진 것을 조합하여 하나의 organisms이 만들어집니다. 
- 회원가입 폼을 유기체로 만든다고 했을 때 이와 같이 만들어집니다.
- ```html
  <Form>
    <InputForm />
    <InputForm />
    <InputForm />
    <InputForm />
    <Button type="submit">회원가입</Button>
    <Button type="reset">취소</Button>
  </Form>
  ```

### templates

- 만들어진 유기체를 합쳐 템플릿을 생성합니다. 템플릿은 그저 화면의 position만 정해줄 뿐 API를 요청한다거나 어떠한 비즈니스 로직이 들어가지 않습니다.
- ```jsx
  <Flex>
    <MainHeader storeInfo={storeInfo} />
    <Flex>
      {children}    
    </Flex>
    <Flex>
      <TermsOfUseFooter storeInfo={storeInfo} />     
    </Flex>
  </Flex>
  ```

### pages

- 페이지는 만들어진 템플릿을 이용해 실제 데이터를 요청하고 화면에 데이터를 뿌리게 됩니다.

## 그래서 Atomic은 어땠나??

- 먼저 개발팀 단독으로 아토믹을 진행하기에는 무리가 있다. 디자인도 아토믹 디자인 패턴을 적용해 원자, 분자, 유기체 기준이 명확히 나와야 한다. 그렇지 않으면 분자와 유기체의 애매모함을 정하느라 시간을 많이 쏟게 될지도 모른다.
- atoms(원자) 설계가 정말 중요한 것 같다. 최대한 많은 `state`를 가지도록 만들었다. 예를 들어 중간정렬 왼쪽정렬 오른쪽정렬 `div`박스를 각각의 `atoms`로 만드는게 아닌 `div`에 넘기는 props값으로 컨트롤 할 수 있도록 했다. 그래야 재사용성이 좋아진다고 느꼈다.
- 그리고 atoms에 최대한 많은 `state`를 가지도록 만들면 전달할 수 있는 props가 많아지는데 이땐 `typescript` 사용하여 혼란스러움을 해결할 수 있다.
- 기존과 다르게 밑에서 위로 설계를 하다보니 어떠한 이벤트 값이 넘어오고 전달되어야 하는지 제대로 알지 못해 작업하면서 필요한 경우 추가적으로 작성했다.
- 주니어 입장에서 느끼기엔 atoms와 molecules는 무조건 재사용성을 생각하며 만들다 보니 처음 개발 기간이 길어질 수 있을 것 같다. 프로토타입을 빨리 만들어야 하는 상황에선 적절치 않은 디자인 패턴 같았다. 하지만 중장기적으로 보면 개발 기간을 단축할 수 있을 것 같다.
- 100% 재사용성에 너무 집착하지 않아도 되는 것 같다. `atoms`는 재사용성이 정말 중요한데 `molecules` 이후 부턴 재사용이 가능할 수도 못할 수도 있다는 것을 인지해야 한다. 대신에 네이밍에 신경을 썼었다. 여기서만 사용될 줄 알았던 분자가 다른 곳에서 사용되는 경우도 있어서 이름을 변경했던 적이 있었다. 
- 아토믹 디자인을 적용하기로 했다면 `Storybook`은 거의 필수?적으로 사용하기를 권장드린다.

## Tailwind CSS와 궁합은 어땠나??

- 궁합이 아주 잘 맞다고 느껴졌다. 디자인에서부터 size와 이런 값들을 약속해놨기 때문에 tailwind.config에서 사이즈를 지정하고 사용하면 됐었다.
  - ```js
     spacing: {
        xxxxs: '0.125rem',
        xxxs: '0.250rem',
        xxs: '0.375rem',
        xs: '0.5rem',
        s: '0.750rem',
        m: '1rem',
        l: '1.250rem',
        xl: '1.5rem',
        xll: '2.0rem',
        xxl: '2.250rem',
        xxxl: '2.5rem'
     }
    ```
- styled-component를 사용했다며 스타일링에 필요한 요소가 없었다면 해당 atoms를 수정해야하는 필요가 있지만 tailwind는 className을 props로 넘겨 간단하게 해결할 수 있었다.
  - ```tsx
    <Flex width={'full'} className={`py-m px-l fixed`}>
    ```
- 하지만 스타일링 요소가 많이 들어가고 네이밍이 길다면 컴포넌트가 복잡해 보이고 가독성이 떨어지는 측면도 있었던 것 같다.
  - ```tsx
    <Flex
      width={'full'}
      alignItems={'start'}
      flexDirection={'col'}
      gapSize={'xxxs'}
      className={'cursor-pointer'} 
      onClick={moveToProductDetail}
    > 
    ```

---

**참고** <br>

