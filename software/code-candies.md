---
title: Code-Candies
layout: default
---
[Home](/) > [Software](/software/index.html) > Code-Candies

# Code-Candies

Hier gibt es eine nette Sammlung von abgefahrenen Code-Snippets, ob
überkomplex, sinnlos oder völlig unleserlich, hier haben alle Snippets einen
Platzt zum Verweilen gefunden, denn aus den Sourcen werden diese schönen
Meisterwerke der Nachtarbeit und des Zeitdruckes nicht lange bestehen dürfen.

Hier ein Snippet aus einem Template, die ohnehin schon schwer zu lesen sind.

{% highlight php %}
<?php
if ($_item->getParentItem()) continue; else $i++;
echo $i%2?'even':'odd'
{% endhighlight %}

Wer bitte ist Schneider und was für eine Bedeutung hat er.

{% highlight php %}
<?php
if(count($itemliste) == 1 && !$this->schneider) {
    $this->format = (int)$itemliste[0]['ofmtID'];
}
{% endhighlight %}


Sinnlose Aneinanderreihung von Operationen die kaum Mehrwert bieten.

{% highlight php %}
<?php
$ret = array_unique(explode(",",join(",",$formats)));
{% endhighlight %}


Warum Datumsfunktionen nutzen, wenn man selber schnell Strings vergleichen kann.

{% highlight php %}
<?php
$dayext = '';
$zeit = date('H:i:s');
if($zeit >= '10:00:00' && $zeit <= '12:00:00')
{   $dayext = " +1 DAY";
}

$this->lieferterminVon = strtotime( substr($pzeit['LieferTerminVon'],0,10).$dayext);
$this->liefertermin = strtotime( substr($pzeit['LieferTerminBis'],0,10).$dayext);
{% endhighlight %}

Die Zahlen im Array beziehen sich auf Primärschlüssel in einer Tabelle, die
könnten also durchaus anders belegt sein als intendiert.

{% highlight php %}
<?php
$expressarten = array(3,6,7,8);
if(in_array($this->versand,$expressarten))
{    $this->liefertermin = $this->lieferterminVon;
}
{% endhighlight %}


Das ist einfach wahnsinnig schwer zu lesen.

{% highlight php %}
<?php
$offsetpreisfaktor = 10.0/9.0;
$this->preis_produktion_aufschlag   = number_format($this->preis_produktion * $offsetpreisfaktor * (1.0 + $mandantenAufschlag/100.0),2,".","");
$this->preis_objekt_aufschlag = number_format($this->preis_objekt * $offsetpreisfaktor * (1.0 + $mandantenAufschlag/100.0),2,".","");
$this->preis_versand_aufschlag  = number_format($this->preis_versand * $offsetpreisfaktor * (1.0 + $mandantenAufschlag/100.0),2,".","");
$this->preis_datenhandling_aufschlag = number_format($this->preis_datenhandling * $offsetpreisfaktor * (1.0 + $mandantenAufschlag/100.0),2,".","");
{% endhighlight %}


Hier besteht immer die Gefahr, dass auf ein Key im Array zugegriffen wird, der
nicht existiert. Und ein Vergleich `count($itemliste) === 1` wäre inhaltlich
leichter nachzuvollziehen.

{% highlight php %}
<?php
if(count($itemliste) <= 1)
{
    if($itemliste[0]['ouID'] != 108)
    {
        $this->setData("activateUmPapier", 1);
    }
}
{% endhighlight %}


Es ist immer leicht an Magento seine eigenen Preise zu berechnen, dass ist aber,
wie in diesem Fall alles andere als dynamisch.

{% highlight php %}
<?php
$res['summe_brutto'] = round($res['summe_netto'] * 1.19, 2);
{% endhighlight %}


Das ist bisher das am schwierigsten zu lesen Beispiel was ich gefunden habe.

{% highlight php %}
<?php
for($i=1; $i<=5; $i++) {
    $groups[
        (!is_null(Mage::getStoreConfig('scoring/group_'.$i.'/from_score') or Mage::getStoreConfig('scoring/group_'.$i.'/from_score') == "") ?
        Mage::getStoreConfig('scoring/group_'.$i.'/from_score') :
        10000 + $i)
        ] = array(
        "id" => $i,
        "status" => Mage::getStoreConfig('scoring/group_'.$i.'/status'),
        "name" => (Mage::getStoreConfig('scoring/group_'.$i.'/name') ?
            Mage::getStoreConfig('scoring/group_'.$i.'/name') :
            Mage::helper('scoring')->__('Group').$i),
        "methods" => Mage::getStoreConfig('scoring/group_'.$i.'/available_payment_methods')
    );
}
{% endhighlight %}


Der Ausdruck liefert immer `false`, kann also auch aus dem Code entfernt
werden.

{% highlight php %}
<?php
if ($_item->getSku() == 'intern_offset' &&  $_item->getSku() == 'intern_digital')
{% endhighlight %}


Eine Inhaltliche Adaption dessen, was die !MySQL Funktion `find_in_set()` tut.

{% highlight php %}
<?php
if($data['filFormat'] != -1)
{       $format = $data['filFormat'];
        $wheres[] = "((opFormat like '%,$format,%' or opFormat like '$format,%' or opFormat like '%,$format') or (opFormat = '$format'))";
}
{% endhighlight %}


Es ist immer gut sprechende Methoden- und Variablenname zu wählen, aber
manchmal versteht man trotz vieler Worte nichts vom gemeinten, so auch hier.

{% highlight php %}
<?php
public function getLastPostInfoPosterForumPosts()
{% endhighlight %}


Man darf ruhig auch mal einen String schreiben, auch wenn Teile davon
Inhaltlich Integer sind, hier castet PHP allerdings automatisch zu String und
man kann sich die vielen Punkte im Code sparen.

{% highlight php %}
<?php
$condition = array(
    'like' => '%' . 1 . '%',
    'like' => '%' . 2 . '%',
    'like' => '%' . 3 . '%',
);
{% endhighlight %}


Sogar in Magento sind schon seit etlichen Versionen Fehler nicht verschwunden.
Hier ein Beispiel aus `Magento` `Mage_Catalog_Model_Product_Type_Grouped` das
die Simple Produkte eines Gruppenproduktes cachen soll, aber nicht tut, weil
`$product` nach dem Ersten Schleifendurchlauf schon lange nicht mehr das
intendierte Gruppenprodukt ist.

Mittlerweile ist der Fehler behoben worden, hat aber etliche Monate gedauert.

{% highlight php %}
<?php
public function getAssociatedProducts($product = null)
{
    if (!$this->getProduct($product)->hasData($this->_keyAssociatedProducts)) {
        ...
        foreach ($collection as $product) {
            $associatedProducts[] = $product;
        }
        $this->getProduct($product)->setData($this->_keyAssociatedProducts, $associatedProducts);
    }
    return $this->getProduct($product)->getData($this->_keyAssociatedProducts);
}
{% endhighlight %}


Interessantes Mapping von Werten, die einen Kommen über eine Schnittstelle, die
anderen sind die hoffentlich entsprechenden `Attribut Ids` im Magento.

{% highlight php %}
<?php
private function convertCondition($condition)
{
    switch ($condition)
    {
        case 11: // neu
            return 136;
        case 1: // wie neu
            return 135;
        case 2: // sehr gut
            return 134;
        case 3: // gut
            return 133;
        case 4: // akzeptabel
        case 5: // ???
            return 132;
        default:
            return $condition;
    }
}
{% endhighlight %}


Ich verrate mal nicht was hier nicht Stimmt, dass sollte offensichtlich sein.
Das `https` war, muss ich eingestehen schön als Klassenkonstante eingebaut,
nur um zu verstehen was hier passiert, habe ich die Konstante in diesem
Snippet ersetzt.

{% highlight php %}
<?php
protected function _isHttpsUrl($url)
{
    $url            = trim($url);
    $urlParts       = str_split($url);
    $httpsUrlParts  = str_split('https');
    foreach ( $httpsUrlParts as $key => $char ) {
        if ( !(isset($urlParts[$key]) && $char == $urlParts[$key]) ) {
            return false;
        }
    }
    return true;
}
{% endhighlight %}


Gleich 2 Varianten die Datenzeilen für einen DATEV export zu generieren,
einmal `str_pad()` und dann gleich in den Code gehackt.

{% highlight php %}
<?php
if($adresse != null)
{
    $datevzeile .= str_pad(substr(utf8_decode($adresse->getData('company')),0,20), 20, ' ', STR_PAD_RIGHT) . ';';
    $datevzeile .= str_pad(substr(utf8_decode($adresse->getStreetFull()),0,36), 36, ' ', STR_PAD_RIGHT) . ';';
    $datevzeile .= str_pad(substr(utf8_decode($adresse->getPostcode()),0,10), 10, ' ', STR_PAD_RIGHT) . ';';
    $datevzeile .= str_pad(substr(utf8_decode($adresse->getCity()),0,30), 30, ' ', STR_PAD_RIGHT) . ';';
}
else
{
    $datevzeile .= '                    ;';
    $datevzeile .= '                                    ;';
    $datevzeile .= '          ;';
    $datevzeile .= '                              ;';
}

$datevzeile .= '        ;';
$datevzeile .= '          ;';
$datevzeile .= '00;';
$datevzeile .= '0,0;';
$datevzeile .= '  ;';
$datevzeile .= ' , ;';
$datevzeile .= '        ;';
{% endhighlight %}


Nur weil PHP recht effizient das Datum parsen kann heißt das nicht, dass man
dass immer wieder tun sollte. Es sollte nur `date('d-m-Y_H-i-s');` genügen.

{% highlight php %}
<?php
$date = date('Y-m-d H:i:s');
$created = date('d-m-Y_H-i-s', strtotime($date));
{% endhighlight %}


Wiedermal sinnlose Vergleiche, die nichts am Programmfluss ändern.

{% highlight php %}
<?php
if($custUpdated < $timeDate && $addUpdated < $timeDate)
{    //continue;
}
{% endhighlight %}


Um vor Verlust vorzubeugen, kann man wichtige Werte gleich in mehreren
Variablen zwischenspeichern, dass kostet zwar Speicher, aber der ist ja billig
zu haben. In diesem Fall wurde `$ordernum` nicht benutzt.

{% highlight php %}
<?php
$ordernum = $order->getData('increment_id');
$crednum = $ordernum;
{% endhighlight %}


Langsam habe ich das Gefühl, dass es vor allem beim Umgang mit zeit und Datum
immer wieder Skurriles zu entdecken gibt.

{% highlight php %}
<?php
$begin = mktime(0, 0, 0, date("m")-1, 1, date("Y"));
$end = strtotime("+1month -1day", $begin);
$dateStart = date('Y-m-d', $begin);
$dateEnd = date('Y-m-d', $end);
{% endhighlight %}


Aus dem Magento, interessante Einrückung, leider alles andere als leserlich
`Mage_Customer_Model_Api_Resource`.

{% highlight php %}
<?php
protected function _isAllowedAttribute($attribute, array $filter = null)
{
    if (!is_null($filter)
        && !( in_array($attribute->getAttributeCode(), $filter)
            || in_array($attribute->getAttributeId(), $filter))) {
        return false;
    }

    return !in_array($attribute->getFrontendInput(), $this->_ignoredAttributeTypes)
        && !in_array($attribute->getAttributeCode(), $this->_ignoredAttributeCodes);
}
{% endhighlight %}


Wusste gar nicht das man einen int-Cast so kompliziert machen kann.

{% highlight php %}
<?php
/**
 * returns an integer value out of an string
 *
 * @param string $string
 */
protected function _getInt($string)
{
    $result = 0;
    foreach ( str_split($string) as $char ) {
        if ( $char === '0' ) {
            $result .= $char;
            continue;
        }
        $int = (int) $char;
        if ( $int ) {
            $result .= $int;
        }
    }
    return (int) $result;
}
{% endhighlight %}


Eine überkomplexe Methode aus Magento (`Mage_Catalog_Model_Product_Indexer_Flat`)

{% highlight php %}
<?php
/**
 * Check if event can be matched by process
 * Overwrote for check is flat catalog product is enabled and specific save
 * attribute, store, store_group
 *
 * @param Mage_Index_Model_Event $event
 * @return bool
 */
public function matchEvent(Mage_Index_Model_Event $event)
{
    if (!Mage::helper('catalog/product_flat')->isBuilt()) {
        return false;
    }

    $data       = $event->getNewData();
    $resultKey = 'catalog_product_flat_match_result';
    if (isset($data[$resultKey])) {
        return $data[$resultKey];
    }

    $result = null;
    $entity = $event->getEntity();
    if ($entity == Mage_Catalog_Model_Resource_Eav_Attribute::ENTITY) {
        /* @var $attribute Mage_Catalog_Model_Resource_Eav_Attribute */
        $attribute      = $event->getDataObject();
        $addFilterable  = Mage::helper('catalog/product_flat')->isAddFilterableAttributes();

        $enableBefore   = ($attribute->getOrigData('backend_type') == 'static')
            || ($addFilterable && $attribute->getOrigData('is_filterable') > 0)
            || ($attribute->getOrigData('used_in_product_listing') == 1)
            || ($attribute->getOrigData('used_for_sort_by') == 1);

        $enableAfter    = ($attribute->getData('backend_type') == 'static')
            || ($addFilterable && $attribute->getData('is_filterable') > 0)
            || ($attribute->getData('used_in_product_listing') == 1)
            || ($attribute->getData('used_for_sort_by') == 1);

        if ($event->getType() == Mage_Index_Model_Event::TYPE_DELETE) {
            $result = $enableBefore;
        } else if ($event->getType() == Mage_Index_Model_Event::TYPE_SAVE) {
            if ($enableAfter || $enableBefore) {
                $result = true;
            } else {
                $result = false;
            }
        } else {
            $result = false;
        }
    } else if ($entity == Mage_Core_Model_Store::ENTITY) {
        if ($event->getType() == Mage_Index_Model_Event::TYPE_DELETE) {
            $result = true;
        } else {
            /* @var $store Mage_Core_Model_Store */
            $store = $event->getDataObject();
            if ($store->isObjectNew()) {
                $result = true;
            } else {
                $result = false;
            }
        }
    } else if ($entity == Mage_Core_Model_Store_Group::ENTITY) {
        /* @var $storeGroup Mage_Core_Model_Store_Group */
        $storeGroup = $event->getDataObject();
        if ($storeGroup->dataHasChangedFor('website_id')) {
            $result = true;
        } else {
            $result = false;
        }
    } else {
        $result = parent::matchEvent($event);
    }

    $event->addNewData($resultKey, $result);

    return $result;
}
{% endhighlight %}


Hier ist der Ausdruck in der if-Anweisung alles andere als einfach zu lesen
`Mage_Catalog_Model_Resource_Eav_Mysql4_Url::_getCategories()`.

{% highlight php %}
<?php
foreach ($rowSet as $row) {
    if (!is_null($storeId) && (strlen($row['path']) > $rootCategoryPathLength) && substr($row['path'], $rootCategoryPathLength, 1) != '/') {
        continue;
    }
    ...
}
{% endhighlight %}


Hier stimmt schon das PHPDOC nicht und dann noch der Test ob der gesuchte wert
in einer kommaseparierten Liste ist - grauenhaft. Mit `explode()` und
`in_array()` würde man den Code besser überblicken können - und er wäre
wahrscheinlich auch schneller.

{% highlight php %}
<?php
/**
 * To check billing country is allowed for the payment method
 *
 * @param string $country country code
 *
 * @return bool
 */
public function canUseForCountry($country)
{
    $groupId = Mage::getSingleton('customer/session')->getCustomer()->getGroupId();
    $allowedGroup = $this->getConfigData('specificgroup');

    if (!strstr($allowedGroup, ','.$groupId)
        and !strstr($allowedGroup, $groupId.',')
        and !strstr($allowedGroup, ','.$groupId.',')
        and ($allowedGroup!=$groupId) ) {
        return false;
    }

    return true;
}
{% endhighlight %}


Hier ein Beitrag zum Thema witzige Fehlermeldungen.

{% highlight php %}
<?php
$kalkRes = $this->kalk->kalkulieren( $_POST );
if ( $kalkRes === false ) {
    throw new Exception("Kalkulation war plötzlich ungültig");
}
{% endhighlight %}


Wieder einmal schwer zu verstehen `Mage_Checkout_Model_Cart`.

{% highlight php %}
<?php
if($minimumQty && $minimumQty > 0 && $request->getQty() < $minimumQty && $quoteProduct === null){
    $request->setQty($minimumQty);
}
{% endhighlight %}


Negationen sind immer etwas schwerer zu lesen `Mage_Sales_Model_Service_Quote`.

{% highlight php %}
<?php
if (!$this->getQuote()->isVirtual() && (!$method || !$rate)) {
    Mage::throwException($helper->__('Please specify a shipping method.'));
}
{% endhighlight %}


Wenn man Referenzen kopiert könnte man sie auch benutzen um die Lesbarkeit zu
erhöhen `Mage_Adminhtml_Model_Sales_Order_Create::createOrder()`.

{% highlight php %}
<?php
if ($this->getSession()->getOrder()->getId()) {
    $oldOrder = $this->getSession()->getOrder();

    $this->getSession()->getOrder()->setRelationChildId($order->getId());
    $this->getSession()->getOrder()->setRelationChildRealId($order->getIncrementId());
    $this->getSession()->getOrder()->cancel()
        ->save();
    $order->save();
}
{% endhighlight %}


Hier hätte man einige Referenzen in Variablen ablegen können
`Mage_Checkout_Model_Type_Multishipping::_prepareOrder()`.

{% highlight php %}
<?php
$item->setProductType($item->getQuoteItem()->getProductType())->setProductOptions($item->getQuoteItem()->getProduct()->getTypeInstance(true)->getOrderOptions($item->getQuoteItem()->getProduct()));
{% endhighlight %}


Der Kommentar erklärt nix, aber auch der Variablenname gibt nicht mehr zu
verstehen `Mage_Sales_Model_Quote_Item`.

{% highlight php %}
<?php
/**
 * Not Represent options
 *
 * @var array
 */
protected $_notRepresentOptions = array('info_buyRequest');
{% endhighlight %}


Da brauche ich nicht viel zu schreiben.

{% highlight php %}
<?php
/**
 *
 * @param bool $bool
 */
public function hasDefaultOption($bool = true)
{
    if (
        (
            Mage::app()->getRequest()->getControllerName() == 'catalog_product'
            && Mage::app()->getRequest()->getActionName() == 'edit'
        )
        ||
        (
            Mage::app()->getRequest()->getControllerName() == 'catalog_category'
        )
        ||
        (
            is_int(stripos(Mage::app()->getRequest()->getControllerName(), 'report'))
        )
        ||
        (
            Mage::app()->getRequest()->getControllerName() == 'dashboard'
        )
    ) {
        $websiteIds = $this->_getHelper()
            ->getWebsiteIdsOfCurrentAdminUser();

        foreach (Mage::app()->getWebsites() as $site) {
            if (!in_array($site->getId(), $websiteIds)) {
                $bool = false;
            }
        }
    }
    return parent::hasDefaultOption($bool);
}
{% endhighlight %}


Hier mal eine Extension von einem Kunden (`abschlussbalken.phtml`)

{% highlight php %}
<?php
<?
if ( !($abschlussbalken = Mage::registry('abschlussbalken')) || $abschlussbalken == '' ) {
    $abschlussbalken = '#ffbc22';
}
?>
<div class="abschlussbalken" style="background: <?=$abschlussbalken?>;">
    &nbsp;
</div>
{% endhighlight %}


Wieder schwer zu lesen - Kategorie Heavy-Function-Nesting.

{% highlight php %}
<?php
$html.= '&empty; ' . number_format(($echoValue)/(max(array($column->getProductCount(), 1))), 2, ',', '.') . ' €';
{% endhighlight %}


Auch nicht besser als obiges Beispiel.

{% highlight php %}
<?php
return $value . ( ($this->getColumn()->getEditOnly() && trim($this->_getValue($row)!='')) ? '' : '</td><td>' ) . $this->_getInputValueElement($row);
{% endhighlight %}


Hier mal Debugging wie bei den Schildbürgern direkt aus dem `git` Repository
von Magento (`Mage_Payment_Helper_Data`). Hier hat wohl jeder Entwickler
seinen eigenen Codeteil zum Debuggen in das `VCS` eingecheckt.

{% highlight php %}
<?php
//        ksort($res);
        //die('!');

        //echo '<pre>';
        //var_dump( (array)$res);
        usort($res, array($this, '_sortMethods'));
        //var_dump((array)$res);
      //  echo '</pre>';
        return $res;
    }

    protected function _sortMethods($a, $b)
    {
       // var_dump($a);
        if (is_object($a)) {
            //var_dump($a->getData());
            //var_dump($a->sort_order);
            //die ();

            return (int)$a->sort_order < (int)$b->sort_order ? -1 : ((int)$a->sort_order > (int)$b->sort_order ? 1 : 0);
        }
        return 0;
    }
{% endhighlight %}


Ich wer' nochmal blede mit dem Scheißding hier - original Formatierung wurde
beibehalten.

{% highlight php %}
<?php
    public function ble($pattern)
{
        if(!is_array($pattern)) {
            $pattern = array($pattern);
        }

         foreach($this->getCollection()->getItems() as $item) {
             foreach($pattern as $singleValueToCheck) {
             #if(stripos($singleValueToCheck, $this->load($id)->getValue()) !== false) {
         #        return true;
             #}
             }
     }

     return false;
    }
{% endhighlight %}


Schöner Kommentar.

{% highlight php %}
<?php
// Fehlermeldungen setzen (Kalkulationsfehler werden immer benötigt)
$this->set_errors($auth_key);
{% endhighlight %}


Hier muss extra erklärt werden, das `}` einen Block beendet
`Mage_Eav_Model_Entity_Attribute_Source_Abstract::getOptionText()`.

{% highlight php %}
<?php
if (sizeof($options) > 0) foreach($options as $option) {
    if (isset($option['value']) && $option['value'] == $value) {
        return isset($option['label']) ? $option['label'] : $option['value'];
    }
} // End
{% endhighlight %}


In dieser Controller-Methode lenkt das exzessive Errorhandling stark von Code ab
des weiteren könnte die Lesbarkeit durch Auslagern der Datenbeschaffung
wesentlich verschlankt werden (Magento `Customer/AccountController`)

{% highlight php %}
<?php
/**
 * Create customer account action
 */
public function createPostAction()
{
    $session = $this->_getSession();
    if ($session->isLoggedIn()) {
        $this->_redirect('*/*/');
        return;
    }
    $session->setEscapeMessages(true); // prevent XSS injection in user input
    if ($this->getRequest()->isPost()) {
        $errors = array();

        if (!$customer = Mage::registry('current_customer')) {
            $customer = Mage::getModel('customer/customer')->setId(null);
        }

        /* @var $customerForm Mage_Customer_Model_Form */
        $customerForm = Mage::getModel('customer/form');
        $customerForm->setFormCode('customer_account_create')
            ->setEntity($customer);

        $customerData = $customerForm->extractData($this->getRequest());

        if ($this->getRequest()->getParam('is_subscribed', false)) {
            $customer->setIsSubscribed(1);
        }

        /**
         * Initialize customer group id
         */
        $customer->getGroupId();

        if ($this->getRequest()->getPost('create_address')) {
            /* @var $address Mage_Customer_Model_Address */
            $address = Mage::getModel('customer/address');
            /* @var $addressForm Mage_Customer_Model_Form */
            $addressForm = Mage::getModel('customer/form');
            $addressForm->setFormCode('customer_register_address')
                ->setEntity($address);

            $addressData    = $addressForm->extractData($this->getRequest(), 'address', false);
            $addressErrors  = $addressForm->validateData($addressData);
            if ($addressErrors === true) {
                $address->setId(null)
                    ->setIsDefaultBilling($this->getRequest()->getParam('default_billing', false))
                    ->setIsDefaultShipping($this->getRequest()->getParam('default_shipping', false));
                $addressForm->compactData($addressData);
                $customer->addAddress($address);

                $addressErrors = $address->validate();
                if (is_array($addressErrors)) {
                    $errors = array_merge($errors, $addressErrors);
                }
            } else {
                $errors = array_merge($errors, $addressErrors);
            }
        }

        try {
            $customerErrors = $customerForm->validateData($customerData);
            if ($customerErrors !== true) {
                $errors = array_merge($customerErrors, $errors);
            } else {
                $customerForm->compactData($customerData);
                $customer->setPassword($this->getRequest()->getPost('password'));
                $customer->setConfirmation($this->getRequest()->getPost('confirmation'));
                $customerErrors = $customer->validate();
                if (is_array($customerErrors)) {
                    $errors = array_merge($customerErrors, $errors);
                }
            }

            $validationResult = count($errors) == 0;

            if (true === $validationResult) {
                $customer->save();

                if ($customer->isConfirmationRequired()) {
                    $customer->sendNewAccountEmail('confirmation', $session->getBeforeAuthUrl());
                    $session->addSuccess($this->__('Account confirmation is required. Please, check your email for the confirmation link. To resend the confirmation email please <a href="%s">click here</a>.', Mage::helper('customer')->getEmailConfirmationUrl($customer->getEmail())));
                    $this->_redirectSuccess(Mage::getUrl('*/*/index', array('_secure'=>true)));
                    return;
                } else {
                    $session->setCustomerAsLoggedIn($customer);
                    $url = $this->_welcomeCustomer($customer);
                    $this->_redirectSuccess($url);
                    return;
                }
            } else {
                $session->setCustomerFormData($this->getRequest()->getPost());
                if (is_array($errors)) {
                    foreach ($errors as $errorMessage) {
                        $session->addError($errorMessage);
                    }
                } else {
                    $session->addError($this->__('Invalid customer data'));
                }
            }
        } catch (Mage_Core_Exception $e) {
            $session->setCustomerFormData($this->getRequest()->getPost());
            if ($e->getCode() === Mage_Customer_Model_Customer::EXCEPTION_EMAIL_EXISTS) {
                $url = Mage::getUrl('customer/account/forgotpassword');
                $message = $this->__('There is already an account with this email address. If you are sure that it is your email address, <a href="%s">click here</a> to get your password and access your account.', $url);
                $session->setEscapeMessages(false);
            } else {
                $message = $e->getMessage();
            }
            $session->addError($message);
        } catch (Exception $e) {
            $session->setCustomerFormData($this->getRequest()->getPost())
                ->addException($e, $this->__('Cannot save the customer.'));
        }
    }

    $this->_redirectError(Mage::getUrl('*/*/create', array('_secure' => true)));
}
{% endhighlight %}


Ganz schön viele eckige Klammern - die Klasse aus der die Zeilen stammten
enthält zudem 35 foreach Schleifen.

{% highlight php %}
<?php
stores = $this->_getAllStoreEntries();
foreach ($stores as $eachRow) {
    $storeViewsArray[$webSiteArray[$eachRow["website_id"]]][$eachRow["store_id"]] = strtoupper(str_replace(" ", "-", $eachRow["name"]));
}
{% endhighlight %}


Sehr schwer zu verstehen und leicht zu missdeuten
`Mage_Adminhtml_Block_Widget_Grid_Column_Renderer_Number`.

{% highlight php %}
<?php
protected function _getValue(Varien_Object $row)
{
    $data = parent::_getValue($row);
    if (!is_null($data)) {
        $value = $data * 1;
        $sign = (bool)(int)$this->getColumn()->getShowNumberSign() && ($value > 0) ? '+' : '';
        if ($sign) {
            $value = $sign . $value;
        }
        return $value ? $value : '0'; // fixed for showing zero in grid
    }
    return $this->getColumn()->getDefault();
}
{% endhighlight %}


Möchte gern mal wissen welcher Entwickler das nach 3 Monaten noch lesen kann
`Mage_Usa_Model_Shipping_Carrier_Ups`.

{% highlight php %}
<?php
if (strlen(trim($response))>0) {
    $rRows = explode("\n", $response);
    $allowedMethods = explode(",", $this->getConfigData('allowed_methods'));
    foreach ($rRows as $rRow) {
        $r = explode('%', $rRow);
        switch (substr($r[0],-1)) {
            case 3: case 4:
                if (in_array($r[1], $allowedMethods)) {
                    $responsePrice = Mage::app()->getLocale()->getNumber($r[8]);
                    $costArr[$r[1]] = $responsePrice;
                    $priceArr[$r[1]] = $this->getMethodPrice($responsePrice, $r[1]);
                }
                break;
            case 5:
                $errorTitle = $r[1];
                break;
            case 6:
                if (in_array($r[3], $allowedMethods)) {
                    $responsePrice = Mage::app()->getLocale()->getNumber($r[10]);
                    $costArr[$r[3]] = $responsePrice;
                    $priceArr[$r[3]] = $this->getMethodPrice($responsePrice, $r[3]);
                }
                break;
        }
    }
    asort($priceArr);
}
{% endhighlight %}


"May the Forse be with you" `Mage_Core_Model_Mysql4_Abstract`.

{% highlight php %}
<?php
/**
 * Forsed save object data
 * forsed update If duplicate unique key data
 *
 * @param Mage_Core_Model_Abstract $object
 * @return Mage_Core_Model_Mysql4_Abstract
 */
public function forsedSave(Mage_Core_Model_Abstract $object)
{% endhighlight %}


Wiedereinmal schwer zu lesen (`Mage_Sales_Model_Order`)

{% highlight php %}
<?php
$this->setData('protect_code', substr(md5(uniqid(mt_rand(), true) . ':' . microtime(true)), 5, 6));
{% endhighlight %}
