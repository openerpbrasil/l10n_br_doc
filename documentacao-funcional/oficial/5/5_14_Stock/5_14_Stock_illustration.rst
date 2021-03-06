
.. index::
   single: Stock; Double-Entry

Understanding Double-Entry Stock Management
===========================================

To illustrate this concept of stock management, see how stock moves are generated by the following
operations:

* Receiving products from a supplier,

* Delivery to a customer,

* Inventory operation for lost materials,

* Manufacturing.

.. index::
   single: module; stock

The structure of stock locations is shown by the figure :ref:`fig-stloctree`. Stocks are assumed to be totally
empty and no operation is in progress nor planned.

If you order '30 bicycles' from a supplier, OpenERP will do the following operations on receipt of the products:

.. table:: Stock Move Operation from Suppliers to Stock

   ================================================== =============
   Location                                           Products
   ================================================== =============
   Partner Locations > Suppliers                      -30 bicycles
   Physical Locations > OpenERP S.A. > Stock          +30 bicycles
   ================================================== =============

If you deliver 2 bicycles to a European customer, you will get the following transactions for the
delivery:

.. table:: Stock Move Operation from Stock to European Customers

   ================================================== =============
   Location                                           Products
   ================================================== =============
   Physical Locations > OpenERP S.A. > Stock          -2 bicycles
   Partner Locations > Customers > European Customers +2 bicycles
   ================================================== =============

When the two operations are complete, you will see the following stock in each location:

.. table:: Resulting Stock Situation

   ================================================== =============
   Location                                           Products
   ================================================== =============
   Partner Locations > Suppliers                      -30 bicycles
   Physical Locations > OpenERP S.A. > Stock          +28 bicycles
   Partner Locations > Customers > European Customers +2 bicycles
   ================================================== =============

So you can see that the sum of the stocks of a product in all the locations in OpenERP is always
zero. In accounting you would say that the sum of the debits is equal to the sum of the credits.

Partner locations (customers and suppliers) are not located under your company in the hierarchical
structure, so their contents are not considered as part of your own stock. So if you just look at
the physical locations inside your own company, those two bicycles are no longer in your company.
Although they are no longer in your own physical stock, it is still very useful to see them in your customer's
stock, because that will help when you carry out detailed stock management analysis.

.. tip:: Consignment Stock

        To manage Consignment Stock, you need to define the location for the consignment customer or supplier as part of your own stock and not as a partner location.

.. note:: Accounts

     In managing stock, a gap between the data in the software and real quantities in stock is
     difficult to avoid.
     Double-entry stock management gives twice as many opportunities to find an error.
     If you forget two items of stock, this error will automatically be reflected in the
     counterpart's location.

You can make a comparison with accounting, where you will easily find an error because you can look
for an anomaly in an account or in the counterparts: if there is not enough in a bank account then that is
probably because someone has forgotten to enter a customer's invoice payment. You always know that the
sum of debits must equal the sum of the credits in both accounting and OpenERP's stock management.

In accounting, all documents lead to accounting entries that form the basis of management
accounting. If you create invoices or enter statements of account, for example, the results of the
operations are accounting entries on accounts. And it is the same for stock management in OpenERP.
All stock operations are carried out as simple stock moves. Whether you pack items, or manufacture
them, or carry out a stock inventory operation, stock moves are carried out every time.

You have seen a fairly simple example of goods receipt and product delivery, but some operations are
less obvious – a stock inventory operation, for example. An inventory operation is carried out
when you compare the stock shown in software with real stock numbers counted in the stores.

.. index::
   single: Stock; Inventory operation
   single: Stock; Stock check

In OpenERP, with its double-entry stock management, you would use stock moves for this inventory
operation. That helps you manage your stock traceability. Suppose there are 26 bicycles in real stock, but
OpenERP shows 28 in the system. You then have to reduce the number in OpenERP to 26. This
reduction of 2 units is considered as a loss or destruction of products and the correction is
carried out as in the following operation:

.. table:: Inventory Operation to Adjust Stock

   ================================================== =============
   Location                                           Products
   ================================================== =============
   Physical Locations > OpenERP S.A. > Stock          -2 bicycles
   Virtual Locations > Inventory Loss                 +2 bicycles
   ================================================== =============

The product stock under consideration then becomes:

.. table:: Real and Counterpart Stocks when Operations are Completed

   ================================================== =============
   Location                                           Products
   ================================================== =============
   Partner Locations > Suppliers                      -30 bicycles
   Physical Locations > OpenERP S.A. > Stock          +26 bicycles
   Partner Locations > Customers > European Customers +2 bicycles
   Virtual Locations > Inventory Loss                 +2 bicycles
   ================================================== =============

This example shows one of the great advantages of this approach in terms of performance analysis.
After a few months, you can just make a stock valuation of the location :menuselection:`Inventory Control --> Location Structure 
--> Virtual Locations --> Inventory Loss` to give you the value of the company's stock losses in the given period.

Now see how the following manufacturing operation is structured in OpenERP. To make a bicycle you
need two wheels and a frame. This means that there should be a reduction of two wheels and a frame
from real stock and the addition of a bicycle there. The consumption / production is formalized by
moving products out of and into physical stock. The stock operations for this are as follows:

.. table:: Stock Situation Resulting from Manufacturing

   ========================================= =========== ================================
   Location                                  Products    Step
   ========================================= =========== ================================
   Physical Locations > OpenERP S.A. > Stock -2 Wheels   Consumption of raw materials
   Virtual Locations > Production            +2 Wheels   Consumption of raw materials
   Physical Locations > OpenERP S.A. > Stock -1 Frame    Consumption of raw materials
   Virtual Locations > Production            +1 Frame    Consumption of raw materials
   Virtual Locations > Production            -1 Bicycle  Manufacture of finished products
   Physical Locations > OpenERP S.A. > Stock +1 Bicycle  Manufacture of finished products
   ========================================= =========== ================================

So now you have got the outcome you need from the consumption of raw materials and the manufacturing of
finished products.

.. note::  Assessing Created Value

    You might already have noticed a useful effect of this approach:
    if you do a stock valuation in the ``Virtual Locations > Production`` location you get
    a statement of value created by your company (as a negative amount).
    Stock valuation in any given location is calculated by multiplying quantities of products in
    stock by their cost.
    In this case, the raw material value is deducted from the finished product value.

.. Copyright © Open Object Press. All rights reserved.

.. You may take electronic copy of this publication and distribute it if you don't
.. change the content. You can also print a copy to be read by yourself only.

.. We have contracts with different publishers in different countries to sell and
.. distribute paper or electronic based versions of this book (translated or not)
.. in bookstores. This helps to distribute and promote the OpenERP product. It
.. also helps us to create incentives to pay contributors and authors using author
.. rights of these sales.

.. Due to this, grants to translate, modify or sell this book are strictly
.. forbidden, unless Tiny SPRL (representing Open Object Press) gives you a
.. written authorisation for this.

.. Many of the designations used by manufacturers and suppliers to distinguish their
.. products are claimed as trademarks. Where those designations appear in this book,
.. and Open Object Press was aware of a trademark claim, the designations have been
.. printed in initial capitals.

.. While every precaution has been taken in the preparation of this book, the publisher
.. and the authors assume no responsibility for errors or omissions, or for damages
.. resulting from the use of the information contained herein.

.. Published by Open Object Press, Grand Rosière, Belgium
