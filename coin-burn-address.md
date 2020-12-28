Cutcoin has a special 'coin burn addres' which can be used to burn coins. If somebody sends coins to this address they can never be spent as the private spend key is not known.
The main functionality is provided by two functions in 'account_utils.cpp' file:

```
void get_coin_burn_address(account_public_address &address, crypto::secret_key &view_secret_key)
{
  crypto::hash seed{coin_burn_seed};
  sc_reduce32(reinterpret_cast<unsigned char*>(seed.data));
  rct::key seed_key = rct::hash2rct(seed);
  view_secret_key = rct::rct2sk(seed_key);
  crypto::secret_key_to_public_key(view_secret_key, address.m_view_public_key);

  crypto::hash h{};
  crypto::cn_fast_hash(seed.data, sizeof(seed.data), h);
  sc_reduce32(reinterpret_cast<unsigned char*>(h.data));
  seed_key = rct::hash2rct(h);
  address.m_spend_public_key = rct::rct2pk(seed_key);
}

account_base get_coin_burn_account()
{
  account_base           cb_acc;
  account_public_address address{};
  crypto::secret_key     view_secret_key;
  get_coin_burn_address(address, view_secret_key);
  cb_acc.create_from_viewkey(address, view_secret_key);
  return cb_acc;
}
```

The code to invoke them and print the results may look as follows:

```
account_base           cb_acc;
account_public_address address{};
crypto::secret_key     view_secret_key;
get_coin_burn_address(address, view_secret_key);
cb_acc.create_from_viewkey(address, view_secret_key);
std::cout << cb_acc.get_public_address_str(network_type::MAINNET) << std::endl;
std::cout << cb_acc.get_keys().m_view_secret_key << std::endl;
std::cout << address.m_view_public_key << std::endl;
std::cout << address.m_spend_public_key << std::endl;
```

The 'get_coin_burn_account' returns the account with the constant address and keys:

```
address           cutbEUhEhaWeG3dRDmWGy8UGLeDsU9EHcEhXGRrXi47NSj2PXpjaMKoce411rzhwggYGFy7MyTy27BMrQm55NNhF5yAm4c1ADi
view public key  <cb610f52bad51212e0ec4aa205bae8e0fe0df555b03def7ca332fbd29a831bbc>
view secret key  <86364a7a4e558ca836cd57aa0e54129d343b3d4347494f53596165676b6d710f>
spend public key <869fa358dfdec268a32fea169ba300e8da06ad0e4751e61daea5429a4599cc0a>
```

It is possible to create the view-only wallet corresponding to coin burn address and explore the history of the transfers. One way to do it is to run

```
./cutcoin-wallet-cli --generate-from-view-key wallet-file-name
```

and follow the instructions.
