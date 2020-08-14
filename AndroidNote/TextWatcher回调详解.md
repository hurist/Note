### beforeTextChanged(CharSequence s, int start, int count, int after) 

在字符输入到输入框之前调用，可以理解为，在字符串s中，从start位置开始，将有count个字符被替换成after个新字符

### onTextChanged(CharSequence s, int start, int before, int count)

从start位置开始，有count个新字符替换了长度为before的久字符

### afterTextChanged(Editable s)

替换完成后的字符串

