# Sample-SMPP-Connection-and-SMS-Sending-with-Python
     import smpplib.client
     import smpplib.consts
     import smpplib.gsm

     # Create SMPP Client
     client = smpplib.client.Client('<IP>', PORT)

     # Connect
     client.connect()

     # TRX bind (both send and receive delivery reports)
     client.bind_transceiver(
         system_id='YOUR_SYSTEM_ID',  # System ID (provided by SMS provider)
         password='YOUR_PASSWORD'     # Password (provided by SMS provider)
     )

     # Send message
     pdu = client.send_message(
         source_addr_ton=smpplib.consts.SMPP_TON_ALNUM,
         source_addr='SENDER_NAME',       # Sender name (max 11 characters)
         dest_addr_ton=smpplib.consts.SMPP_TON_INTL,
         destination_addr='905xxxxxxxxx', # Recipient phone number in international format
         short_message='Hello bro, this is a test SMS',
         data_coding=0,  # 0 = Latin, 8 = Unicode
         esm_class=0
     )

     print(f"Message sequence: {pdu.sequence}")

     # Unbind and disconnect
     client.unbind()
     client.disconnect()
