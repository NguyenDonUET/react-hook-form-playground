## 🤔 Cách valida mảng động các input?

- tạo biến `form = useForm({resolver: valibotResolver(adCopySchema)})`

- trong adCopySchema: ràng buộc cho mỗi element, ràng buộc cho cái mảng

```js
  listHeadline: array(
    string('Headline can not be empty', [
      minLength(5, 'Character limit (5~30)'),
      maxLength(MAX_LENGTH.AD_COPY.HEADLINE, 'Character limit (5~30)'),
      noFourConsecutiveIdenticalChars,
    ]),
    [
      minLength(1, 'Headline is required'),
      maxLength(MAX_HEADLINES, `No more than ${MAX_HEADLINES} headlines are allowed`),
    ],
  ),


```

- kiểu của form: `UseFormReturn<AdCopy, any, undefined>`

- getValues của form

- lấy headlines: `headlines = getValues('listHeadline') || [''];` và in ra các InputCheck(có check icon nếu khác chuỗi rỗng)

- khi register cho InputCheck: là input thường

  ```js
  {...register(`listHeadline.${index}`)}`
  ```

- khi click add new input => addHeadline('')

```js
setValue('listHeadline', [...getValues('listHeadline'), headline]);
// focus vào input cuối cùng
form.setFocus(`listHeadline.${headlines.length}`);
```

- hiện message lỗi:

```js
  error={errors.listHeadline?.[index]?.message}
  errors.listHeadline?.root là true
```
