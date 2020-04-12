## Curve notes

### Koblitz curve

#### Jacobian坐标系

Jacobian Coordinates are used to represent elliptic curve points on prime curves `y^2 = x^3 + ax + b`.
They give a speed benefit over Affine Coordinates when the cost for field inversions is significantly
higher than field multiplications. In Jacobian Coordinates the triple (X, Y, Z) represents the affine
point (X / Z^2, Y / Z^3).

#### Affine坐标系

https://mathworld.wolfram.com/AffineCoordinates.html

{O, e1, e2, e3} 仿射坐标系。
当e1, e2, e3为单位向量时，成为笛卡尔坐标系。
当e1, e2, e3相互垂直时， 成为直角坐标系。

在secp256k1, affine坐标系其实就是指代(x, y)，用于描述椭圆曲线上的一个点。

#### 坐标系转换

**Jacobian => Affine**

x = X/Z^2, y = Y/Z^3

**Affine => Jacobian**

X = x, Y = y, Z = 1

#### 代数计算

在Affine坐标系下，P1 = (x1, y1), P2 = (x2, y2), P=P1+P2

x3 = ((y2-y1)/(x2-x1))^2-x1-x2
y3 = (y2-y1)/(x2-x1)*(x1-x3) - y1

化简可得：

x3 = ((3x1^2+a)/2y1)^2 - 2x1        I+2M+S
y3 = (3x1^2+a)/2y1 * (x1-x3) - y1   I+2M+2S

在Jacobian坐标系下，E = Y^2 = X^3+axZ^4+bZ^6

求P=P1+P2                     12M+6S

x3=u^2-v^3-2x1z2^2v^2
y3=u*(x1 * z2^2 * v^2 - x3) - y1z2^3v^3
z3=vz1*z2

其中 u = y2z1^3 - y1z2^3
    v = x2z1^2 - x1z2^2

求P = 2P(x1, y1, z1)            4M+6S (可以不进行Inversion计算)

x3=(3x1^2+az1^4)^2 - 8x1y1^2
y3=(3x1^2+az1^4)(4x1y1^2-x3) - 8y1^4
z3=2y1z1

http://hyperelliptic.org/EFD/g1p/auto-shortw-jacobian-0.html#addition-mmadd-2007-bl

#### NAF

todo

