# secret_sauce-1
standard_user
git clone <repo-url>
cd saucedemo-tests
npm install
npx wdio run wdio.conf.js
npx wdio run wdio.conf.js --spec ./test/specs/login.spec.js
saucedemo-tests/
 ├── test/
 │    ├── pageobjects/
 │    │    ├── LoginPage.js
 │    │    ├── InventoryPage.js
 │    │    ├── CartPage.js
 │    │    └── CheckoutPage.js
 │    └── specs/
 │         ├── login.spec.js
 │         ├── cart.spec.js
 │         └── checkout.spec.js
 └── wdio.conf.js
 class LoginPage {
    get inputUsername() { return $('#user-name'); }
    get inputPassword() { return $('#password'); }
    get btnLogin() { return $('#login-button'); }
    get errorMessage() { return $('.error-message-container'); }

    async login(username, password) {
        await this.inputUsername.setValue(username);
        await this.inputPassword.setValue(password);
        await this.btnLogin.click();
    }
}
module.exports = new LoginPage();
class InventoryPage {
    get inventoryItems() { return $$('.inventory_item'); }
    get cartIcon() { return $('.shopping_cart_badge'); }

    async addItemToCart(itemIndex = 0) {
        const addBtn = await this.inventoryItems[itemIndex].$('button');
        await addBtn.click();
    }

    async openCart() {
        await $('.shopping_cart_link').click();
    }
}
module.exports = new InventoryPage();
class CartPage {
    get cartItems() { return $$('.cart_item'); }
    get btnCheckout() { return $('#checkout'); }

    async removeItem(itemIndex = 0) {
        const removeBtn = await this.cartItems[itemIndex].$('button');
        await removeBtn.click();
    }

    async proceedToCheckout() {
        await this.btnCheckout.click();
    }
}
module.exports = new CartPage();
class CheckoutPage {
    get inputFirstName() { return $('#first-name'); }
    get inputLastName() { return $('#last-name'); }
    get inputZip() { return $('#postal-code'); }
    get btnContinue() { return $('#continue'); }
    get btnFinish() { return $('#finish'); }
    get successMessage() { return $('.complete-header'); }

    async checkout(firstName, lastName, zip) {
        await this.inputFirstName.setValue(firstName);
        await this.inputLastName.setValue(lastName);
        await this.inputZip.setValue(zip);
        await this.btnContinue.click();
        await this.btnFinish.click();
    }
}
module.exports = new CheckoutPage();
