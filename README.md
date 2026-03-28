import React, { useState } from "react";
      {/* Header */}
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-3xl font-bold">HAMAJ Store</h1>
        <Button onClick={() => setShowCart(!showCart)}>
          <ShoppingCart className="mr-2" /> ({cart.length})
        </Button>
      </div>

      {/* Search & Filter */}
      <div className="flex gap-4 mb-6">
        <div className="flex items-center border rounded-xl px-3 w-full">
          <Search />
          <Input
            placeholder="Search products..."
            value={search}
            onChange={(e) => setSearch(e.target.value)}
            className="border-none"
          />
        </div>
        <select
          className="border rounded-xl p-2"
          onChange={(e) => setCategory(e.target.value)}
        >
          <option>All</option>
          <option>Men</option>
          <option>Women</option>
          <option>Kids</option>
        </select>
      </div>

      {/* Products */}
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {filtered.map((product) => (
          <Card key={product.id} className="rounded-2xl shadow-lg">
            <CardContent className="p-4">
              <img src={product.image} alt={product.name} className="w-full rounded-xl mb-4" />
              <h2 className="text-xl font-semibold">{product.name}</h2>
              <p className="text-gray-600">Rs. {product.price}</p>
              <Button className="mt-4 w-full" onClick={() => addToCart(product)}>
                Add to Cart
              </Button>
            </CardContent>
          </Card>
        ))}
      </div>

      {/* Cart Drawer */}
      {showCart && (
        <div className="fixed right-0 top-0 w-80 h-full bg-white shadow-2xl p-4">
          <h2 className="text-xl font-bold mb-4">Your Cart</h2>
          {cart.length === 0 ? (
            <p>No items</p>
          ) : (
            cart.map((item, i) => (
              <div key={i} className="flex justify-between mb-2">
                <span>{item.name}</span>
                <span>Rs. {item.price}</span>
              </div>
            ))
          )}
          <hr className="my-4" />
          <p className="font-bold">Total: Rs. {total}</p>

          <Button className="w-full mt-4" onClick={sendWhatsAppOrder}>
            Order via WhatsApp
          </Button>
        </div>
      )}
    </div>
  );
}

