# Emoji
Emoji所有有序的表情极其编码 

-(void)setupKeyboardView{
    UIView *view = [[UIView alloc]initWithFrame:CGRectMake(0, kScreenHeight - 300, 300, 300)];
    
    NSArray *emojiArray = [Emoji allEmoji];
    for (NSInteger i = 0; i < emojiArray.count; i ++) {
        UIButton *button =[[UIButton alloc]init];
        button.frame = CGRectMake(i%8 * (kScreenwidth/8.0), i/8 * (kScreenwidth/8), kScreenwidth/8, kScreenwidth/8);
        [button setTitle:emojiArray[i] forState:UIControlStateNormal];
        [button addTarget:self action:@selector(println:) forControlEvents:UIControlEventTouchUpInside];
        [view addSubview:button];
    }
    view.backgroundColor =[UIColor redColor];
    [self.view addSubview:view];
    
}
  
  
  
  
    
    

打印出来表情编码：
NSString *hexstr = @"";  
  
    for (int i=0;i< [text length];i++)  
    {  
        hexstr = [hexstr stringByAppendingFormat:@"%@",[NSString stringWithFormat:@"0x%1X ",[text characterAtIndex:i]]];  
    }  
    NSLog(@"UTF16 [%@]",hexstr);  
      
    hexstr = @"";  
      
    int slen = strlen([text UTF8String]);  
      
    for (int i = 0; i < slen; i++)   
    {  
        //fffffff0 去除前面六个F & 0xFF   
        hexstr = [hexstr stringByAppendingFormat:@"%@",[NSString stringWithFormat:@"0x%X ",[text UTF8String][i] & 0xFF ]];  
    }  
    NSLog(@"UTF8 [%@]",hexstr);  
      
    hexstr = @"";  
      
    if ([text length] >= 2) {  
          
        for (int i = 0; i < [text length] / 2 && ([text length] % 2 == 0) ; i++)   
        {  
            // three bytes  
            if (([text characterAtIndex:i*2] & 0xFF00) == 0 ) {  
                hexstr = [hexstr stringByAppendingFormat:@"Ox%1X 0x%1X",[text characterAtIndex:i*2],[text characterAtIndex:i*2+1]];  
            }  
            else  
            {// four bytes    
                hexstr = [hexstr stringByAppendingFormat:@"U+%1X ",MULITTHREEBYTEUTF16TOUNICODE([text characterAtIndex:i*2],[text characterAtIndex:i*2+1])];      
            }  
              
        }  
        NSLog(@"(unicode) [%@]",hexstr);  
    }  
    else  
    {  
        NSLog(@"(unicode) U+%1X",[text characterAtIndex:0]);  
    }  
