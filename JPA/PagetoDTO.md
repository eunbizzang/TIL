https://stackoverflow.com/questions/39036771/how-to-map-pageobjectentity-to-pageobjectdto-in-spring-data-rest


 Page.map without lambda expressions:

```
Page<ObjectEntity> entities = objectEntityRepository.findAll(pageable);
Page<ObjectDto> dtoPage = entities.map(new Converter<ObjectEntity, ObjectDto>() {
    @Override
    public ObjectDto convert(ObjectEntity entity) {
        ObjectDto dto = new ObjectDto();
        // Conversion logic

        return dto;
    }
});
```

In Spring Data 2, the Page map method takes a Function instead of a Converter

Using Function:

```
Page<ObjectEntity> entities = objectEntityRepository.findAll(pageable);
Page<ObjectDto> dtoPage = entities.map(new Function<ObjectEntity, ObjectDto>() {
    @Override
    public ObjectDto apply(ObjectEntity entity) {
        ObjectDto dto = new ObjectDto();
        // Conversion logic

        return dto;
    }
});
```


in java8:

```
Page<ObjectDto> entities = 
 objectEntityRepository.findAll(pageable)
 .map(ObjectDto::fromEntity);
 ```

I used package method