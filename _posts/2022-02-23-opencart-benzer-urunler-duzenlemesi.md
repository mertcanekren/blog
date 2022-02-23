---
layout: post
title: Opencart Benzer Ürünler Düzenlemesi
date: 2022-02-23 20:00:00 +0530
description: Opencart ürün detay sayfasına benzer ürünleri gösterme.
categories: opencart
---

Opencart üzerinde ürün sayfasında gösterilen ürün ile aynı kategoride olan ürünlerin otomatik ve random olarak gösterimi için eklediğim düzenlemeleri yapabilirsiniz.

catalog/controller/product/product.php dosyası içerisine $this->model_catalog_product->getProductRelated satırından sonra aşağıda olan kodu ekleyin.
```php
if(count($results)<3){// gösterim yapmak istediğiniz ürün sayısı
    $temp = $this->model_catalog_product->getProductRelatedByCategory($this->request->get['product_id'],count($results));
    foreach($temp as $t){               
    if(!empty($t)){                 
        $results[] = $t;                
        }        
    }        
}   
```

catalog/model/catalog/product.php dosyası içerisinde $product_data[$result['related_id']] = $this->getProduct satırından sonra aşağıda olan kodu ekleyin.
```php
public function getProductRelatedByCategory($product_id,$num_results) {
    $product_data = array();
        $num = 3 - $num_results;// gösterim yapmak istediğiniz ürün sayısı 
        $getCat = $this->db->query("SELECT * FROM " . DB_PREFIX . "product_to_category WHERE product_id = '" . (int)$product_id . "'");     $query = $this->db->query("SELECT * FROM " . DB_PREFIX . "product_to_category WHERE category_id = '" . (int)$getCat->row['category_id'] . "' AND product_id != '" . (int)$product_id . "' ORDER BY RAND() LIMIT 0,".$num."");                       
        foreach ($query->rows as $result) {
            $product_data[$result['product_id']] = $this->getProduct($result['product_id']);
    }   
    return $product_data;
} 
```