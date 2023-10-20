- [jasnell web streams in node](https://www.jasnell.me/posts/webstreams)
```js
import { ReadableStream, WritableStream } from 'node:stream/web';

function getSomeSource() {
  let count = 0;
  const  maxCount = 5;
  return {
    start(controller) {
      // This is called when the readable stream is constructed
    },
    pull(controller) {
      // This is called when the consumer wants to read data
      
      if(count < maxCount) {
        controller.enqueue(`some data; count: ${count}`);
        count++;
      } else {
        controller.close();
      }
    },
    cancel(reason) {
      // This is called when the consumer cancels the stream
    }
  };
}

function getSomeSink() {
  return {
    start(controller) {
      // This is called when the writable stream is constructed
    },
    write(chunk, controller) {
      // This is called when the consumer writes data
      console.log(chunk);
    },
    close(controller) {
      // This is called when the consumer closes the stream
    },
    abort(reason) {
      // This is called when the consumer aborts the stream
    }
  };
}

(async () => {
  
  const readable = new ReadableStream(getSomeSource());
  const writable = new WritableStream(getSomeSink());
  
  await readable.pipeTo(writable);
})();


// import {
//   ReadableStream,
//   WritableStream
// } from 'node:stream/web';

// const readable = new ReadableStream(getSomeSource());
// const writable = new WritableStream(getSomeSink());

// await readable.pipeTo(writable);

```

### Transform
```js
import { ReadableStream, WritableStream, TransformStream } from 'node:stream/web';

function getSomeSource() {
  let count = 0;
  const  maxCount = 5;
  return {
    start(controller) {
      // This is called when the readable stream is constructed
    },
    pull(controller) {
      // This is called when the consumer wants to read data
      
      if(count < maxCount) {
        controller.enqueue(`some data; count: ${count}`);
        count++;
      } else {
        controller.close();
      }
    },
    cancel(reason) {
      // This is called when the consumer cancels the stream
    }
  };
}

function getSomeTransform(){
  return {
    transform(chunk, controller) {
      controller.enqueue(`${chunk.toUpperCase()} yes hello this is dog`);
    }
  }
}

// const transform = new TransformStream({
//   transform(chunk, controller) {
//     controller.enqueue(chunk.toUpperCase());
//   }
// });
// const transform = new TransformStream({
//   start(controller) {
//     // Called immediately when the TransformStream is created
//   },

//   transform(chunk, controller) {
//     // Called for every chunk received by the WritableStream
//     // side. The chunk is modified, then forwarded on to the
//     // ReadableStream side via the controller.
//   },

//   flush(controller) {
//     // Called when the WritableStream side has finished
//     // forwarding chunks on to the transformer.
//   }
// });

function getSomeSink() {
  return {
    start(controller) {
      // This is called when the writable stream is constructed
    },
    write(chunk, controller) {
      // This is called when the consumer writes data
      console.log(chunk);
    },
    close(controller) {
      // This is called when the consumer closes the stream
    },
    abort(reason) {
      // This is called when the consumer aborts the stream
    }
  };
}

(async () => {
  const readable = new ReadableStream(getSomeSource());
  const writable = new WritableStream(getSomeSink());
  const transform = new TransformStream(getSomeTransform());
  await readable.pipeThrough(transform).pipeTo(writable);
})();

```

> Checkpoint AI
> Q: is it accurate regarding web streams in node: a ReadableStream's pull operation will only run to fill the queue once the promise is resolved
> A: Yes, your understanding is accurate. In the Web Streams API, the `pull()` method is invoked by a `ReadableStream` whenever its internal data queue isn't full, and more data is needed. If the `pull()` method returns a promise, it won't be called again until the promise is resolved. This mechanism provides a natural backpressure model, preventing consumers from reading data from the source faster than it's available【8†source】.

- utility function for pulling (downloading) data into a web stream queue
```js
// utils.mjs
export function getSomeSource() {
  let count = 0;
  const  maxCount = 5;
  return {
    start(controller) {
    },
    pull(controller) {
      if(count < maxCount) {
        controller.enqueue(`some data; count: ${count}`);
        count++;
      } else {
        controller.close();
      }
    },
    cancel(reason) {
    }
  };
}
```

- converting a web stream to node stream and reading it in node
```js
import {
  Readable
} from 'node:stream';
import {getSomeSource} from "./utils.mjs"; 
const readable = new ReadableStream(getSomeSource()); // web stream
const nodeReadable = Readable.fromWeb(readable); // convert web stream to node stream
nodeReadable.on('data', console.log); 
```


- converting a node stream to web stream and reading it (in node)
```js
import { Readable } from 'node:stream';

const readable = new Readable({
  read(size) {
    this.push(Buffer.from('hello'));
  }
});

const readableStream = Readable.toWeb(readable);
const reader = readableStream.getReader();
const result = await reader.read();
console.log(result.value.toString());
```