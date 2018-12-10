---
title:  "OpenCV에서 프로세싱한 이미지 Tesseract에서 사용하기"
permalink: "/:categories/discrete-math-fundamentals"
date: 2015-10-21 01:00:00 +0900
categories: [C++]
tags: [Programming, C++, OpenCV, cycle]
typora-root-url: C:\Users\Myeongwon\source\repos\auspic7.github.io
---

팀 프로젝트를 진행하다가 Input이 이미지나 Pix가 아닌 Mat으로 주어져야 하는 상황에 직면했다. TessBaseAPI는 Mat를 절대로 알아먹을 수 없기에 중간에 형변환하는 것은 피할 수 없는 선택이었고, 여러 가지 포럼을 찾아본 끝에 해답을 찾아냈다. StackOverflow에 나온 컨버팅 방법은 왜인지 GetUTF8Text에서 오류를 뿜어냈고(Pix로 변환하는 과정에서 몇 가지의 속성이 초기화되지 않은 것으로 보인다), 해답은 직접 TessBaseAPI에 SetImage를 해 주는 것이었다. 다음은 그 소스코드이다.
```C++

//

//  main.cpp

//  tesseractOCR

//

//  Created by Myeongwon on 2015. 10. 21..

//  Copyright © 2015년 Myeongwon. All rights reserved.

//







#include <tesseract/baseapi.h>

#include <leptonica/allheaders.h>

#include <opencv2/core/core.hpp> 

#include <opencv2/highgui/highgui.hpp>

#include <opencv2/imgproc/imgproc.hpp>

#include <iostream>



using namespace cv;

using namespace std;

int _mat();

Pix *pixtes;

tesseract::TessBaseAPI api;



int main()

{

    char *outText;

    

    _mat();

    

    outText = api.GetUTF8Text();

    printf("OCR output:\n%s", outText);

    namedWindow( "Display window", WINDOW_AUTOSIZE );



    // 메모리 릴리즈

    api.End();

    delete [] outText;

    

    pixDestroy(&pixtes);

    

    return 0;

}



int _mat(){

        

    Mat image = imread("%__imagepath__", CV_LOAD_IMAGE_COLOR);   // 파일을 MAT에 입력



    printf("%d",  image.depth() == CV_8U);

    namedWindow( "Display window", WINDOW_AUTOSIZE );

    imshow( "Display window", image );

    // 이미지 로딩

    

    cv::Mat gray;

    cv::cvtColor(image, gray, CV_BGR2GRAY);

    // 개략적인 전처리

    

    // Tesseract API로 입력시킴. Pix자료형으로 바꿀 수 있을...까?

    api.Init(NULL, "eng", tesseract::OEM_DEFAULT);

    api.SetPageSegMode(tesseract::PSM_SINGLE_BLOCK);

    api.SetImage((uchar*)gray.data, gray.cols, gray.rows, 1, gray.cols);

    api.Recognize(0);

    waitKey(0);                

    

    return 0;



}
```

