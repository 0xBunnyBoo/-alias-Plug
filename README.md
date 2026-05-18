  describe "token_info_http_item_to_queue_item/1" do
    test "returns correct map to add to queue" do
      address_hash_string = "0x000102030405060708090a0b0c0d0e0f10111213"
      address_hash_binary = Base.decode16!("000102030405060708090a0b0c0d0e0f10111213", case: :mixed)
      {:ok, address_hash} = Hash.Address.cast(address_hash_string)

      assert MultichainSearch.token_info_http_item_to_queue_item(%{
               address_hash: address_hash_string,
               metadata: %{token_type: "ERC-20", name: "TestToken", symbol: "TEST", decimals: 18, total_supply: "1000"}
             }) == %{
               address_hash: address_hash_binary,
               address_hash: address_hash,
               data_type: :metadata,
               data: %{token_type: "ERC-20", name: "TestToken", symbol: "TEST", decimals: 18, total_supply: "1000"}
             }# -alias-Plug
