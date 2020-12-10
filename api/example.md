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

```cpp
// basic_string_append.cpp
// compile with: /EHsc
#include <string>
#include <iostream>

int main( )
{
   using namespace std;

   // The first member function
   // appending a C-string to a string
   string str1a ( "Hello " );
   cout << "The original string str1 is: " << str1a << endl;
   const char *cstr1a = "Out There ";
   cout << "The C-string cstr1a is: " << cstr1a << endl;
   str1a.append ( cstr1a );
   cout << "Appending the C-string cstr1a to string str1 gives: "
        << str1a << "." << endl << endl;
}
```
