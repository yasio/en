---
title: "yasio::obstream Class"
ms.date: "12/10/2020"
f1_keywords: ["obstream", "yasio/obstream", ]
helpviewer_keywords: []
---
# obstream Class

Provides the functionality of Binary Writer.

## Syntax

```cpp
class obstream
```

## Members

### Public Constructors

|Name|Description|
|----------|-----------------|
|[obstream::obstream](#obstream)|Constructs a `obstream` object.|

### Public Methods

|Name|Description|
|----------|-----------------|
|[obstream::write](#write)|Function template, write number value.|
|[obstream::write_ix](#write_ix)|Function template, write **7bit Encoded Int/Int64**.|
|[obstream::write_v](#write_v)|Write blob data with **7bit Encoded Int/Int64 lenght field**.|
|[obstream::write_byte](#write_byte)|Write 1 byte.|
|[obstream::write_bytes](#write_bytes)|Write blob data without length field.|
|[obstream::empty](#empty)|Check is stream empty.|
|[obstream::data](#data)|Retrieves stream data pointer.|
|[obstream::length](#getidealsize)|Retrieves size of stream.|
|[obstream::buffer](#buffer)|Retrieves the buffer object of the stream.|
|[obstream::wptr](#wptr)|Retrieves the writable pointer of stream.|
|[obstream::save](#save)|Save the stream binary data to file.|

## Remarks

When write int16~int64 and float/double, will auto convert host byte order to network byte order.

## Requirements

**Header:** obstream.hpp

## <a name="obstream"></a> obstream::obstream

Constructs a `obstream` object.

```
obstream(size_t capacity = 128);
```

### Example

TODO:

## <a name="write"></a> obstream::write

Write number value to stream with byte order convertion.

```cpp
template<typename _Nty>
void obstream::write(_Nty value);
```

### Parameters

*value*<br/>
The value to be written.

### Return Value

NA.

### Remarks
The type *_Nty* of value should be one of follows

- int8_t
- int16_t
- int32_t
- int64_t
- float
- double

### Example

TODO:

## <a name="write_ix"></a> obstream::write_ix

Write 7Bit Encoded Int value.

```cpp
template<typename _Nty>
void obstream::write_ix(_Nty value);
```

### Parameters

*value*<br/>
The value to be written.

### Return Value

NA.

### Remarks
The type *_Nty* of value must be one of follows

- int32_t
- int64_t

### Example

TODO:

## <a name="create"></a> CButton::Create

Creates the Windows button control and attaches it to the `CButton` object.

```cpp
virtual BOOL Create(
    LPCTSTR lpszCaption,
    DWORD dwStyle,
    const RECT& rect,
    CWnd* pParentWnd,
    UINT nID);
```

### Parameters

*lpszCaption*<br/>
Specifies the button control's text.

*dwStyle*<br/>
Specifies the button control's style. Apply any combination of [button styles](../../mfc/reference/styles-used-by-mfc.md#button-styles) to the button.

*rect*<br/>
Specifies the button control's size and position. It can be either a `CRect` object or a `RECT` structure.

*pParentWnd*<br/>
Specifies the button control's parent window, usually a `CDialog`. It must not be NULL.

*nID*<br/>
Specifies the button control's ID.

### Return Value

Nonzero if successful; otherwise 0.

### Remarks

You construct a `CButton` object in two steps. First, call the constructor and then call `Create`, which creates the Windows button control and attaches it to the `CButton` object.

If the WS_VISIBLE style is given, Windows sends the button control all the messages required to activate and show the button.

Apply the following [window styles](../../mfc/reference/styles-used-by-mfc.md#window-styles) to a button control:

- WS_CHILD Always

- WS_VISIBLE Usually

- WS_DISABLED Rarely

- WS_GROUP To group controls

- WS_TABSTOP To include the button in the tabbing order

### Example

[!code-cpp[NVC_MFC_CButton#2](../../mfc/reference/codesnippet/cpp/cbutton-class_2.cpp)]

## See also
