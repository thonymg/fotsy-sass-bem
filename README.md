# Fotsy Sass Bem — mixins for easily writing BEM selector in Sass/Scss - 
##Mixin pour ecrire facilement des sélecteurs BEM en Sass/Scss.


* Note: Don't work with libSass and Sass < 3.4.

## Install & Use

1. Clone `fotsy-sass-bem` somewhere to your project:

    ```sh
    git clone https://github.com/thonymg/fotsy-sass-bem.git
    ```
2. Include it in your main Scss file:

    ```Sass
    @import "tmg-bem";
    ```

3. Simple exemple:

    ```Sass
    .block1{
      @include e(element1){
        content: "element 1";
        
        @include m(modifier1){
          content: "modifier 1";
        }
      }
    }

    ```

    would render to something like

    ```Css
    .block1__element1 {
          content: "element 1";
    }
    .block1__element1--modifier1 {
      content: "modifier 1";
    }
    ```

## The nesting

1. .block3 inside .block2 and .element2

    ```Sass
    .block1{
      @include e(element1){
        content: "element 1";
        .block2{
          @include e(element2){
            content: "element 2";
            
            @include m(modifier2){
              content: "modifier 2";
            }
          
            .block3{
              @include e(element3){
                content: "element 2";
                
                @include m(modifier3){
                  content: "modifier 2";
                }
              }
            }
          }
        }
      }
    } 
    ```

    would render to something like

    ```Css
    .block1__element1 {
      content: "element 1";
    }
    .block2__element2 {
      content: "element 2";
    }
    .block2__element2--modifier2 {
      content: "modifier 2";
    }
    .block3__element3 {
      content: "element 2";
    }
    .block3__element3--modifier3 {
      content: "modifier 2";
    }
    ```

2. .block3 inside block2 but not inside .element2

    ```Sass
    .block1{
      @include e(element1){
        content: "element 1";
        .block2{
          @include e(element2){
            content: "element 2";
            
            @include m(modifier2){
              content: "modifier 2";
            }
          }
            .block3{
              @include e(element3){
                content: "element 3";
                
                @include m(modifier3){
                  content: "modifier 3";
                }
              }
            }
          
        }
      }
    } 
    ```

    would render to something like

    ```Css
    .block1__element1 {
      content: "element 1";
    }
    .block2__element2 {
      content: "element 2";
    }
    .block2__element2--modifier2 {
      content: "modifier 2";
    }
    .block2 .block3__element3 {
      content: "element 3";
    }
    .block2 .block3__element3--modifier3 {
      content: "modifier 3";
    }

    ```

3. With @media query

    ```Sass
    .block1{
      @include e(element1){
        content: "element 1";
        
        @media screen and (min-width: 40em) {
          .block2{
            @include e(element2){
              content: "element 2";
              
              @include m(modifier2){
                content: "modifier 2";
              }
      
              .block3{
                @include e(element3){
                  content: "element 3";
                  
                  @include m(modifier3){
                    content: "modifier 3";
                  }
                }
              }
            }
          }
        }
      }
    }  
    ```

    would render to something like

    ```Css
    .block1__element1 {
      content: "element 1";
    }

    @media screen and (min-width: 40em) {
      .block2__element2 {
        content: "element 2";
      }
      .block2__element2--modifier2 {
        content: "modifier 2";
      }
      .block3__element3 {
        content: "element 3";
      }
      .block3__element3--modifier3 {
        content: "modifier 3";
      }
    }

    ```

4. With @media query and .block3 outside .element2

    ```Sass
    .block1{
      @include e(element1){
        content: "element 1";
        
        @media screen and (min-width: 40em) {
          .block2{
            @include e(element2){
              content: "element 2";
              
              @include m(modifier2){
                content: "modifier 2";
              }
            }
            
              .block3{
                @include e(element3){
                  content: "element 3";
                  
                  @include m(modifier3){
                    content: "modifier 3";
                  }
                }
              }
            
          }
        }
      }
    }  
    ```

    would render to something like

    ```Css
    .block1__element1 {
      content: "element 1";
    }
    @media screen and (min-width: 40em) {
      .block2__element2 {
        content: "element 2";
      }
      .block2__element2--modifier2 {
        content: "modifier 2";
      }
      .block2 .block3__element3 {
        content: "element 3";
      }
      .block2 .block3__element3--modifier3 {
        content: "modifier 3";
      }
    }
    ```

## The 2nd Parameter

###If you need inception. Add 'false' to the 2nd parameter of the @mixin element

1. .block3 inside .block2 and .element2

    ```Sass
     .block1{
      @include e(element1){
        content: "element 1";
          .block2{
            @include e(element2, false){
              content: "element 2";              
              @include m(modifier2){
                content: "modifier 2";
              }
                        
              .block3{
                @include e(element3){
                  content: "element 3";                  
                  @include m(modifier3){
                    content: "modifier 3";
                  }
                }
              }            
          }
        }
      }
    } 
    ```


    would render to something like

    ```Css
    .block1__element1 {
      content: "element 1";
    }
    .block1__element1 .block2__element2 {
      content: "element 2";
    }
    .block1__element1 .block2__element2--modifier2 {
      content: "modifier 2";
    }
    .block2__element2 .block3__element3 {
      content: "element 3";
    }
    .block2__element2 .block3__element3--modifier3 {
      content: "modifier 3";
    }
    } 
    ```


2. .block3 inside block2 but not inside .element2

    ```Sass
    .block1{
      @include e(element1){
        content: "element 1";
          .block2{
            @include e(element2, false){
              content: "element 2";              
              @include m(modifier2){
                content: "modifier 2";
              }
            }            
            .block3{
              @include e(element3){
                content: "element 3";                  
                @include m(modifier3){
                  content: "modifier 3";
                }
              }
            }            
          
        }
      }
    } 
    ```


    would render to something like

    ```Css
    .block1__element1 {
      content: "element 1";
    }
    .block1__element1 .block2__element2 {
      content: "element 2";
    }
    .block1__element1 .block2__element2--modifier2 {
      content: "modifier 2";
    }
    .block2 .block3__element3 {
      content: "element 3";
    }
    .block2 .block3__element3--modifier3 {
      content: "modifier 3";
    }

    ```

    - - -
### my other project
my library for responsive typography [soratra-responsive](https://github.com/thonymg/soratra-responsive)


more mixins soon !!!!

Je suis un peuple d'Anosibe. [follow Anosibe on twitter](https://twitter.com/anosibe/).
Or [follow me on twitter](https://twitter.com/thonyMg/).

* Paix et guérrisons pour les tiens. 

- - -
