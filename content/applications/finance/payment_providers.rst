class SaleOrderInherit(models.Model):
    _inherit = 'sale.order'

    payment_method = fields.Selection([
        ('bank', 'Bank Transfer'),
        ('cash_on_delivery', 'Cash on Delivery'),
        ('vodafone_cash', 'Vodafone Cash')  # Adding Vodafone Cash
    ], string="Payment Method", required=True)

    def action_confirm(self):
        super(SaleOrderInherit, self).action_confirm()

        if self.payment_method == 'bank':
            message = "Thank you for your order. Please make the payment to bank account XYZ."
            self.send_payment_message(message)
        elif self.payment_method == 'cash_on_delivery':
            message = "Thank you for your order. Please have the cash ready upon delivery."
            self.send_payment_message(message)
        elif self.payment_method == 'vodafone_cash':
            message = "Thank you for your order. Please make the payment via Vodafone Cash and send a screenshot of the payment to 01022665469."
            self.send_payment_message(message)

    def send_payment_message(self, message):
        # This method will handle sending the payment message to the customer
        # You can adjust this to send an email, or a notification, etc.
        pass

