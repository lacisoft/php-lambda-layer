# PHP Layer For AWS Lambda

Ever want to run PHP websites in AWS Lambda? It's your lucky day!

**:warning: This is an experimental AWS Lambda Layer and Runtime. It should not be used for production services. Obligatory legal statement follows:**

> STACKERY INC. AND/OR ITS RESPECTIVE SUPPLIERS MAKE NO REPRESENTATIONS ABOUT THE SUITABILITY, RELIABILITY, AVAILABILITY, TIMELINESS, AND ACCURACY OF THE INFORMATION, SOFTWARE, PRODUCTS, SERVICES AND RELATED GRAPHICS CONTAINED ON THE MSN WEB SITES FOR ANY PURPOSE. ALL SUCH INFORMATION, SOFTWARE, PRODUCTS, SERVICES AND RELATED GRAPHICS ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND. MICROSOFT AND/OR ITS RESPECTIVE SUPPLIERS HEREBY DISCLAIM ALL WARRANTIES AND CONDITIONS WITH REGARD TO THIS INFORMATION, SOFTWARE, PRODUCTS, SERVICES AND RELATED GRAPHICS, INCLUDING ALL IMPLIED WARRANTIES AND CONDITIONS OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. IN NO EVENT SHALL MICROSOFT AND/OR ITS SUPPLIERS BE LIABLE FOR ANY DIRECT, INDIRECT, PUNITIVE, INCIDENTAL, SPECIAL, CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER INCLUDING, WITHOUT LIMITATION, DAMAGES FOR LOSS OF USE, DATA OR PROFITS, ARISING OUT OF OR IN ANY WAY CONNECTED WITH THE USE OR PERFORMANCE OF THE MSN WEB SITES, WITH THE DELAY OR INABILITY TO USE THE MSN WEB SITES OR RELATED SERVICES, THE PROVISION OF OR FAILURE TO PROVIDE SERVICES, OR FOR ANY INFORMATION, SOFTWARE, PRODUCTS, SERVICES AND RELATED GRAPHICS OBTAINED THROUGH THE MSN WEB SITES, OR OTHERWISE ARISING OUT OF THE USE OF THE MSN WEB SITES, WHETHER BASED ON CONTRACT, TORT, NEGLIGENCE, STRICT LIABILITY OR OTHERWISE, EVEN IF MICROSOFT OR ANY OF ITS SUPPLIERS HAS BEEN ADVISED OF THE POSSIBILITY OF DAMAGES. BECAUSE SOME STATES/JURISDICTIONS DO NOT ALLOW THE EXCLUSION OR LIMITATION OF LIABILITY FOR CONSEQUENTIAL OR INCIDENTAL DAMAGES, THE ABOVE LIMITATION MAY NOT APPLY TO YOU. IF YOU ARE DISSATISFIED WITH ANY PORTION OF THE MSN WEB SITES, OR WITH ANY OF THESE TERMS OF USE, YOUR SOLE AND EXCLUSIVE REMEDY IS TO DISCONTINUE USING THE MSN WEB SITES.

### Usage
Simply configure your function as follows:

1. Set the `Runtime` to `provided`
1. Determine the latest version of the layer: `aws lambda list-layer-versions --layer-name arn:aws:lambda:<your region>:887080169480:layer:php71`
1. Add the following Lambda Layer: `arn:aws:lambda:<your region>:887080169480:layer:php71:<latest version>`

If you are using AWS SAM it's even easier! Update your function:

```yaml
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      ...
      Runtime: provided
      Layers:
        - !Sub arn:aws:lambda:${AWS::Region}:887080169480:layer:php71
```

### Development

The layer is built by:

1. Installing a Docker environment
1. Running `make` in the layers directory

This will launch a Docker container that will build php71.zip.