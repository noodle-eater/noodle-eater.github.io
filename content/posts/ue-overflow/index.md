---
title: "Unreal Engine Overflow"
date: 2022-05-06T21:42:25+07:00
draft: false
---

Recently, I start using Unreal Engine to develop games. I did not have proper C++ or Unreal Engine knowledge, I usually use Unity and C#. while learn and use it, I stumbled across some problems. So I decide to make some notes that I can use and share with other.

---

### Print `Enum` Into `FString`

```cpp
StaticEnum<ENUM_TYPE>()->GetValueAsString(ENUM_VALUE)
```

### Format `FText`

```cpp
FText format = "Item Name: {ItemName}"
const FText formattedText = FText::FormatNamed(FTextFormat(format), TEXT("ItemName"), itemName);
```

### Loop `UDataTable`

```cpp
itemDT->ForeachRow<FItemInfo>("FindItem", [&](const FName& key, const FItemInfo& item) {
    // Do something here
});
```

### Find a Row in `UDataTable`

```cpp
FItemInfo* itemInfo = itemDT->FindRow<FItemInfo>(ROW_NAME, "FindItem");
```

### Create `UObject` Instance

```cpp
UTextBlock* text = NewObject<UTextBlock>(btn, FName("text"));
```

### Hide Field on Certain Condition

```cpp
UPROPERTY(EditAnywhere, meta=(Condition="YOUR_CONDITION", EditConditionHides))
float speed;
```

### Create Min Max Slider for Field

```cpp
UPROPERTY(EditAnywhere, meta = (ClampMin = "1", ClampMax = "10"))
int32 totalSpawned;
```

---

The code above is not tested, and used for reference purpose. I hope it will be helpful, I hope I can update it again in the future.

Cheers 😊
