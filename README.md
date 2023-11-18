# data-structures-linked-list
data structures linked list with C programming (adding, deleting, inserting elements, adding sequential elements and deleting elements.)- C programlama ile veri yapılarında bağlı listeler. bağlı listelerden eleman silme, sıralı eleman ekleme, başa ve sona eleman ekleme ve silme işlemleri

- ****Bağlı Listeler (Linked List)****
    
    linked listin ilk elemanı mutlaka tutulmalı yoksa bağlı listeye ulaşılmaz ve zamanda kaybolur.
    
    Bağlı listeler doğrusal - sequential access olarak erişilebilir.
    
    Arrayler ise random access olarak erişilir yanı rastgele bir elemana erişilebilir.
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>  // malloc kullanmak için gerekli
    
    struct n{
        int x;
        n * next;
    };
    typedef n node; //n denildiginde node u ifade ede.
    
    int main() {
        node * root;
        root = (node *)malloc(sizeof(node));
        root -> x=10; //ilk nodun değeri 10 olur.
        root -> next= (node *) malloc (sizeof(node)); // ilk elemandan sonra bir node daha oluşturur.
        root -> next -> x=20; //yeni dügümün degeri atandı.
        
        // bu sekilde tek tek node olusturmak pratik degil.
        //bundan dolayıbir root dahatutuyoruz ancak buna 
        // node * iter diyoruz.
        //iter burada dolasmayı saglar.ve istenen degeri point edebilir.
        
        node*iter;
        iter=root;
        printf("%d",iter->x);
        iter=iter->next;
        printf("%d",iter->x);
        
        return 0;
    }
    
    //bu kod sonucunda 10 ve 20 yazar
    ```
    
    node *iter olayının görseli;
    
   ![image](https://github.com/ispirbanu/data-structures-linked-list/assets/45195137/153a8b27-da3e-4b3e-af9a-0768ec0006b2)

    
    ```c
    Struct node yazılmadan derlemedi
    // Online C compiler to run C program online
    #include <stdio.h>
    #include <stdlib.h>  // malloc kullanmak için gerekli
    
    struct node{
        int x;
        struct node * next;
    };
    // typedef n node; //n denildiginde node u ifade ede.
    
    int main() {
        struct node * root;
        root = (struct node *)malloc(sizeof(struct node));
        root -> x=10; //ilk nodun değeri 10 olur.
        root -> next= (struct node *) malloc (sizeof(struct node)); // ilk elemandan sonra bir node daha oluşturur.
        root -> next -> x=20; //yeni dügümün degeri atandı.
        
        // bu sekilde tek tek node olusturmak pratik degil.
        //bundan dolayıbir root dahatutuyoruz ancak buna 
        // node * iter diyoruz.
        //iter burada dolasmayı saglar.ve istenen degeri point edebilir.
        
        struct node*iter;
        iter=root;
        printf("%d",iter->x);
        iter=iter->next;
        printf("%d",iter->x);
        
        return 0;
    }
    ```
    
    ## Döngü ile bağlı liste
    
    ```c
    //listeyi bastırmak için bir fonk 
    void bastir(struct node * r){
        while(r!=NULL){
            printf("%d \n",r->x);
            r=r->next;
        }
    }
    
    iter=root;
    // iter boşluk gösterene kadar listede gezinmek. son elemana gelene kadar hareket etmektir.
        // ancak iter null olmamalı iter->next null olana kadar kontrol sağlanmalı
        // aksi halde null olduğunda ekleme yapılamaz.
        //liste içinde gezinmek
    	//bu kod bloğu da yazdırmaya yarar üstteki fonk ile aynı
        while (iter->next !=NULL ){
            printf("%d \n",iter->x);
            iter= iter->next;
        }
    
    // döngü ile yeni veriler eklemek
    for (int i=0; i<5; i++){
            iter->next=(struct node *) malloc(sizeof(struct node));
            iter= iter-> next;
            iter->x= i*5;
            iter->next=NULL;
            // iter sonuna null elle eklenmeli. 
        }
        bastir(root);
    ```
    
    ## Sona ekleme işlemini de fonk içerisinde yaparsak ;
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        int x;
        struct node * next;
    };
    // typedef n node; //n denildiginde node u ifade ede.
    
    void bastir(struct node * r){
        while(r!=NULL){
            printf("%d \n",r->x);
            r=r->next;
        }
    }
    void ekle(struct node *r, int x){
        while(r->next !=NULL){
            r=r->next;
        }
        r->next = (struct node *)malloc(sizeof(struct node*));
        r->next ->x=x;
        r->next-> next =NULL;
    }
    
    int main() {
        struct node * root;
        root=(struct node*) malloc(sizeof(struct node));
        root-> next=NULL;
        root ->x=10;
        for (int i=0; i<5; i++){
           ekle(root,i*5);
        }
        bastir(root);
        
        return 0;
    }
    ```
    
    Bu işlemde dikkat edilmesi gereken nokta for içerisinde belli değerleri eklemesi için fonksiyona veriyoruz ancak fonksiyon içerisinde her seferinde baştan başlayıp son düğüme kadar gidip ekliyor yani baştan sona her ekleme işleminde döner ve performans açısından daha kötüdür üstteki kod parşasındaki for ile eklemek aslında buna göre daha iyi performans verir.
    
    ## Bağlı listede araya ekleme
    
    Oluşturduğumuz listede 3. düğümden sonra bir eleman eklemek isteyelim. Önce baştan 3 eleman hareket ederiz. ardından bağımsız temp olarak bir düğüm oluştururuz ardından da bu geçici elemanı araya eklemek için iterdeki elemanın nextinde bulunanları geçici elemanın nexti olarak atarız önce bunu yapmamız önemlidir aksi halde diğer ögeleri kaybederiz.
    
    Ardından da iter elemanının nextini bu yeni eleman olarak atarız. ve bu düğümün değerini veririz.
    
    ```c
    struct node *iter=root;
        for(int i=0; i<3; i++){
            iter=iter->next;
        }
        struct node * temp =(struct node *)malloc(sizeof(struct node));
        temp->next=iter->next;
        iter->next=temp;
        temp->x=100;
        bastir(root);
    ```
    
    ### ****Sıralı Ekleyen Fonksiyon****
    
    ```c
    //bu fonksiyonda değişiklik olduğunda r üzerinden değişiklerin ana listedeği düğümü de etkilemesi gerekiyor bu yüzden bu değeri dönderen fonkiyon oluşturulur.
    struct node* ekleSirali(struct node* r, int x){
        
        //hiç eleman yoksa
        if(r==NULL){
            r=(struct node*) malloc(sizeof(struct node));
            r-> next=NULL;
            r->x=x;
            return r;
        }
    //bir eleman varsa ve gelen değer ilk elemandan küçükse soluna eklenir
    //yani kök değişir.
        if(r->x >x){
            struct node * temp =(struct node *)malloc(sizeof(struct node));
            temp->x=x;
            temp->next=r;
            r=temp;
            return r;
        }
        
        //araya eklenecekse aralık bulunması gerekiyorsa
        //listenin sonunda değilse ve gelen eleman arada bir elemandan büyükse sonrasına eklenecek
        // en büyük elemansa null görene kadar yada kendinden büyük eleman görene kadar devam ederek araya ekleyecek
     
        struct node * iter = r;  // r döndürüldüğü için bir geçiçi iter değeri oluşturulur
        while(iter->next !=NULL && iter->next->x <x){
            iter=iter->next;
        }
        struct node * temp= (struct node *)malloc(sizeof(struct node));
        temp->next =iter ->next;
        iter->next =temp;
        temp->x=x;
        return r;
    }
    
    int main() {
        struct node * root;
        root=NULL;
        //root= ekleSirali yapmamızın nedeni fonk başında yazıldı.
        root= ekleSirali(root,400);
        root= ekleSirali(root,200);
        root=ekleSirali(root,350);
        root= ekleSirali(root,50);
        root= ekleSirali(root,450);
        
        bastir(root);
        
        return 0;
    }
    
    sonuc;
    50 
    200 
    350 
    400 
    450
    ```
    
    ## Silme işlemi
    
    ```c
    struct node* sil(struct node* r,int x){
        struct node * iter = r;
        struct node *temp;
        
        //baştaki elemanı silmedurumu
        if(r->x ==x){
            temp=r;
            r=r->next;
            free(temp);
            return r;
        }
        // istenilen bir elemanı silme
        
        while(iter->next !=NULL && iter->next->x !=x){
            iter=iter->next;
        }
        //sonuna kadar gelindiyse ve sayı yoksa
        if(iter->next==NULL){
            return r;
        }
        // c de otomatik olarak hafızada bir çö toplama olmaz bu yüzden silinecek düğümün pointırı ile elle silmemiz gerekir.
        // bu durum için bir temp var elemanı tutan 
        // ardından silinecek elemandan sonraki değerleri kaybetmemek için gerekli atamalar yapılır sonra da silinir (free)
        temp=iter->next;
        iter->next =iter->next->next;
        free(temp);
        return r;
    }
    
    int main() {
        struct node * root;
        root=NULL;
        //root= ekleSirali yapmamızın nedeni fonk başında yazıldı.
        root= ekleSirali(root,400);
        root= ekleSirali(root,200);
        root=ekleSirali(root,30);
        root= ekleSirali(root,50);
        root= ekleSirali(root,350);
        root= ekleSirali(root,450);
        bastir(root);
        
        root=sil(root,400);
    
        bastir(root);
        
        return 0;
    }
    
    //     sonuç;
    // ekleme
    // 30   
    // 50 
    // 200 
    // 350 
    // 400 
    // 450
    
    // silme 
    // 30 
    // 50 
    // 200 
    // 350 
    // 450
    ```
