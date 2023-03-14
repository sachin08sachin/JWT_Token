

<h1> JWT - Javascript Object Notation(JSON) Web Token 😎</h1>
<h2>What is JSON web token?</h2>
<p>               securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA. 
  <br>
Although JWTs can be encrypted to also provide secrecy between parties, we will focus on signed tokens. Signed tokens can verify the integrity of the claims contained within it, while encrypted tokens hide those claims from other parties. When tokens are signed using public/private key pairs, the signature also certifies that only the party holding the private key is the one that signed it.</p>
<br>
<h2>When should you use JSON Web Tokens?</h2>
<blockquote>
<p>Here are some scenarios where JSON Web Tokens are useful:…</p>
<blockquote>
  <p><strong>Authorization: </strong> This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token. Single Sign On is a feature that widely uses JWT nowadays, because of its small overhead and its ability to be easily used across different domains.</p>
  <p><strong>Information Exchange:</strong> JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are. Additionally, as the signature is calculated using the header and the payload, you can also verify that the content hasn't been tampered with.</p>

</blockquote>
</blockquote>
<h2><h2>When should you use JSON Web Tokens?</h2></h2>
<p>In its compact form, JSON Web Tokens consist of three parts separated by dots (.), which are:</p>
                              <uL><li>Header</li><li>Payload</li><li>Signature</li></ul>
                              <p>Therefore, a JWT typically looks like the following.</p>
                              <code>xxxxx.yyyyy.zzzzz</code>
                              <p>Let's break down the different parts.</p>
                              <h3>Header</h3>
                              <p>The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.</p>
                              <p>For example:</p>
                              <code>{
  "alg": "HS256",
  "typ": "JWT"
}</code>
<p>Then, this JSON is <strong><em> Base64Url</em></strong> encoded to form the first part of the JWT.</p>
<h3>Payload</h3>
<p>The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.</p>
<h4>Registered claims:</h4>
<p>These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: <b>iss</b> (issuer), <b>exp</b> (expiration time), <b>sub</b> (subject), <b>aud</b> (audience), and others.</p>
  <em>Notice that the claim names are only three characters long as JWT is meant to be compact.</em>
<h4>Public claims:</h4>
<p>These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.</p>
<h4>Private claims</h4>
<p>These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.</p>
<br>
<p>An example payload could be:</p>
<code>
{
  "sub": "1234567890",
  "name": "Naveen Prasath",
  "admin": true
}
</code>
<p>The payload is then <strong><em> Base64Url</em></strong> encoded to form the second part of the JSON Web Token.</p>
<em>Do note that for signed tokens this information, though protected against tampering, is readable by anyone. Do not put secret information in the payload or header elements of a JWT unless it is encrypted.</em>
<h3>Signature</h3>
<p>To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:</P>
<code>HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)</code>
<p>The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.</p>
<b>Putting all together</b>
<p>The output is three Base64-URL strings separated by dots that can be easily passed in HTML and HTTP environments, while being more compact when compared to XML-based standards such as SAML.</P>
<p>The following shows a JWT that has the previous header and payload encoded, and it is signed with a secret. </P>
